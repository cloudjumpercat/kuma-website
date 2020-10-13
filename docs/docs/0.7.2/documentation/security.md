# Security

Kuma helps you secure your existing infrastructure with mTLS. The following sections cover details of how it works.

## Certificates

Kuma uses a built-in CA (Certificate Authority) to issue certificates for dataplanes. The root CA certificate is unique for each mesh
in the system. On Kubernetes, the root CA certificate is stored as a [Kubernetes Secret](https://kubernetes.io/docs/concepts/configuration/secret/).
On Universal, we leverage the same storage (Postgres) that is used for storing policies.
Certificates for dataplanes are ephemeral, re-created on dataplane restart and never persisted on disk.

Dataplane certificates generated by Kuma are X.509 certificates that are [SPIFFE](https://github.com/spiffe/spiffe/blob/master/standards/X509-SVID.md) compliant. The SAN of certificate is set to `spiffe://<mesh name>/<service name>`

Kuma also supports other CAs. For further details refer to [Mutual TLS](../../policies/mutual-tls) policy.

## Dataplane Authentication

In order to obtain an mTLS certificate from the server ([SDS](https://www.envoyproxy.io/docs/envoy/latest/configuration/security/secret) built-in in the control plane), a dataplane must authenticate itself.

:::: tabs :options="{ useUrlFragment: false }"

::: tab "Kubernetes (Service Account Token)"
On Kubernetes, a dataplane proves its identity by leveraging [ServiceAccountToken](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/#service-account-automation) that is mounted in every pod.
:::

::: tab "Universal (Dataplane Token)"

On Universal, a dataplane must be explicitly configured with a security token (Dataplane Token) that will be used to prove its identity.
Dataplane Token is a signed [JWT token](https://jwt.io) that carries data of the dataplane that is allowed to join the mesh.
It is signed by an RSA key auto-generated by the control plane on the first run. Tokens are not stored in the control plane,
the only thing that is stored is a signing key that is used for token verification and generation. 

You can generate token either by REST API
```bash
curl -XPOST \ 
  -H "Content-Type: application/json" \
  --data '{"name": "dp-echo-1", "mesh": "default", "tags": {"kuma.io/service": ["backend", "backend-admin"]}}' \
  http://localhost:5679/tokens
```

or by using `kumactl`
```bash
kumactl generate dataplane-token \
  --name dp-echo-1 \
  --mesh default \
  --tag kuma.io/service=backend,backend-admin > /tmp/kuma-dp-echo1-token
``` 

The token should be stored in a file and then used when starting `kuma-dp`
```bash
$ kuma-dp run \
  --name=dp-echo-1 \
  --mesh=default \
  --cp-address=http://127.0.0.1:5681 \
  --dataplane-token-file=/tmp/kuma-dp-echo-1-token
```

You can also pass Dataplane Token as `KUMA_DATAPLANE_RUNTIME_TOKEN` Environment Variable. 

#### Dataplane Token boundary

As you can see in the example above, you can generate a token by passing name, mesh, and tags. Control Plane will verify Dataplane against data available in the Token. This means you can generate a token by specifying:
* only `mesh`. This way you can reuse the token for all dataplanes in a given mesh.
* `mesh` + `tag` (ex. `kuma.io/service`). This way you can use one token across all instances of given service.
  Keep in mind that you have to specify all the values. If you have a Dataplane with 2 inbounds, one with `kuma.io/service: backend` and one with `kuma.io/service: backend-admin`, you need to specify both values (`--tag kuma.io/service=backend,backend-admin`).
* `mesh` + `name` + `tag` (ex. `kuma.io/service`). This way you can use one token for one instance of given service.


#### Turn off authentication

You can turn off authentication for testing proposes. Set `KUMA_ADMIN_SERVER_APIS_DATAPLANE_TOKEN_ENABLED` to `false`.

::: warning
If you turn off authentication, any dataplane can request certificate for any service, therefore this should not be used in a production setup.
:::
::::

### Accessing Admin Server from a different machine

By default, the Admin Server that is serving Dataplane Tokens is exposed only on `localhost`. If you want to generate tokens from a different machine than the control plane you have to secure the connection:
1) Enable public server by setting `KUMA_ADMIN_SERVER_PUBLIC_ENABLED` to `true`. Make sure to specify hostname which can be used to access Kuma from other machine via `KUMA_GENERAL_ADVERTISED_HOSTNAME`.
2) Generate certificate for the HTTPS Admin Server and set via `KUMA_ADMIN_SERVER_PUBLIC_TLS_CERT_FILE` and `KUMA_ADMIN_SERVER_PUBLIC_TLS_KEY_FILE` config environment variable.
   For generating self-signed certificate you can use `kumactl`
```bash
$ kumactl generate tls-certificate --cert-file=/path/to/cert --key-file=/path/to/key --type=server --cp-hostname=<name from KUMA_GENERAL_ADVERTISED_HOSTNAME>
```
3) Pick a public interface on which HTTPS server will be exposed and set it via `KUMA_ADMIN_SERVER_PUBLIC_INTERFACE`.
   Optionally pick the port via `KUMA_ADMIN_SERVER_PUBLIC_PORT`. By default, it will be the same as the port for the HTTP server exposed on localhost.
4) Generate one or more certificates for the clients of this server. Pass the path to the directory with client certificates (without keys) via `KUMA_ADMIN_SERVER_PUBLIC_CLIENT_CERTS_DIR`.
   For generating self-signed client certificates you can use `kumactl`
```bash
$ kumactl generate tls-certificate --cert-file=/path/to/cert --key-file=/path/to/key --type=client
```
5) Configure `kumactl` with client certificate.
```bash
$ kumactl config control-planes add \
  --name <NAME> --address http://<KUMA_CP_DNS_NAME>:5681 \
  --admin-client-cert <CERT.PEM> \
  --admin-client-key <KEY.PEM>
```

### Multizone

When running in multizone mode you can generate tokens both on Global and Remote Control Plane
If you configure your deployment pipeline to generate Dataplane Token before running a dataplane you can use Remote CP. This way Global CP is not a single point of failure.

::: tip
If you are running Global CP on Kubernetes and trying to generate tokens. Port forward `5679` and `5681` ports first and then use `kumactl` (or `curl`) to generate tokens.
:::

## mTLS

Once a dataplane has proved its identity, it will be allowed to fetch its own identity certificate and a root CA certificate of the mesh.
When establishing a connection between two dataplanes each side validates each other dataplane certificate confirming the identity using the root CA of the mesh.

mTLS is _not_ enabled by default. To enable it, apply proper settings in [Mesh](../../policies/mesh) policy.
Additionally, when running on Universal you have to ensure that every dataplane in the mesh has been configured with a Dataplane Token.

When mTLS is enabled, every connection between dataplanes is denied by default, so you have to explicitly allow it using [TrafficPermission](../../policies/traffic-permissions).

## Postgres

Since on Universal, the secrets such as "provided" CA's private key, are stored in Postgres, a connection between Postgres and Kuma CP should be secured with TLS.
To secure the connection, first pick the security mode using `KUMA_STORE_POSTGRES_TLS_MODE`. There are several modes:
* `disable` - is not secured with TLS (secrets will be transmitted over network in plain text).
* `verifyNone` - the connection is secured but neither hostname, nor by which CA the certificate is signed is checked.
* `verifyCa` - the connection is secured and the certificate presented by the server is verified using the provided CA.
* `verifyFull` - the connection is secured, certificate presented by the server is verified using the provided CA and server hostname must match the one in the certificate.

The CA for verification server's certificate can be set using `KUMA_STORE_POSTGRES_TLS_CA_PATH`.

Once secured connections are configured in Kuma CP, you have to configure Postgres' [`pg_hba.conf`](https://www.postgresql.org/docs/9.1/auth-pg-hba-conf.html) file to restrict unsecured connections.
Here is an example configuration that will allow only TLS connections and will require username and password:
```
# TYPE  DATABASE        USER            ADDRESS                 METHOD
hostssl all             all             0.0.0.0/0               password
```
 
You can also provide client key and certificate for mTLS using `KUMA_STORE_POSTGRES_TLS_CERT_PATH` and `KUMA_STORE_POSTGRES_TLS_KEY_PATH`.
This pair can be used for auth-method `cert` described [here](https://www.postgresql.org/docs/9.1/auth-pg-hba-conf.html).