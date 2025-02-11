---
title: kumactl get
---

Show Kuma resources

### Synopsis

Show Kuma resources.

### Options

```
  -h, --help            help for get
  -o, --output string   output format: one of table|yaml|json (default "table")
```

### Options inherited from parent commands

```
      --api-timeout duration   the timeout for api calls. It includes connection time, any redirects, and reading the response body. A timeout of zero means no timeout (default 1m0s)
      --config-file string     path to the configuration file to use
      --log-level string       log level: one of off|info|debug (default "off")
      --no-config              if set no config file and config directory will be created
```

### SEE ALSO

* [kumactl](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl)	 - Management tool for Kuma
* [kumactl get circuit-breaker](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_circuit-breaker)	 - Show a single CircuitBreaker resource
* [kumactl get circuit-breakers](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_circuit-breakers)	 - Show CircuitBreaker
* [kumactl get dataplane](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_dataplane)	 - Show a single Dataplane resource
* [kumactl get dataplanes](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_dataplanes)	 - Show Dataplane
* [kumactl get external-service](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_external-service)	 - Show a single ExternalService resource
* [kumactl get external-services](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_external-services)	 - Show ExternalService
* [kumactl get fault-injection](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_fault-injection)	 - Show a single FaultInjection resource
* [kumactl get fault-injections](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_fault-injections)	 - Show FaultInjection
* [kumactl get global-secret](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_global-secret)	 - Show a single GlobalSecret resource
* [kumactl get global-secrets](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_global-secrets)	 - Show GlobalSecret
* [kumactl get healthcheck](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_healthcheck)	 - Show a single HealthCheck resource
* [kumactl get healthchecks](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_healthchecks)	 - Show HealthCheck
* [kumactl get mesh](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_mesh)	 - Show a single Mesh resource
* [kumactl get meshaccesslog](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshaccesslog)	 - Show a single MeshAccessLog resource
* [kumactl get meshaccesslogs](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshaccesslogs)	 - Show MeshAccessLog
* [kumactl get meshcircuitbreaker](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshcircuitbreaker)	 - Show a single MeshCircuitBreaker resource
* [kumactl get meshcircuitbreakers](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshcircuitbreakers)	 - Show MeshCircuitBreaker
* [kumactl get meshes](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshes)	 - Show Mesh
* [kumactl get meshfaultinjection](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshfaultinjection)	 - Show a single MeshFaultInjection resource
* [kumactl get meshfaultinjections](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshfaultinjections)	 - Show MeshFaultInjection
* [kumactl get meshgateway](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshgateway)	 - Show a single MeshGateway resource
* [kumactl get meshgatewayroute](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshgatewayroute)	 - Show a single MeshGatewayRoute resource
* [kumactl get meshgatewayroutes](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshgatewayroutes)	 - Show MeshGatewayRoute
* [kumactl get meshgateways](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshgateways)	 - Show MeshGateway
* [kumactl get meshhealthcheck](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshhealthcheck)	 - Show a single MeshHealthCheck resource
* [kumactl get meshhealthchecks](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshhealthchecks)	 - Show MeshHealthCheck
* [kumactl get meshhttproute](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshhttproute)	 - Show a single MeshHTTPRoute resource
* [kumactl get meshhttproutes](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshhttproutes)	 - Show MeshHTTPRoute
* [kumactl get meshproxypatch](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshproxypatch)	 - Show a single MeshProxyPatch resource
* [kumactl get meshproxypatches](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshproxypatches)	 - Show MeshProxyPatch
* [kumactl get meshratelimit](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshratelimit)	 - Show a single MeshRateLimit resource
* [kumactl get meshratelimits](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshratelimits)	 - Show MeshRateLimit
* [kumactl get meshretries](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshretries)	 - Show MeshRetry
* [kumactl get meshretry](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshretry)	 - Show a single MeshRetry resource
* [kumactl get meshtimeout](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshtimeout)	 - Show a single MeshTimeout resource
* [kumactl get meshtimeouts](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshtimeouts)	 - Show MeshTimeout
* [kumactl get meshtrace](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshtrace)	 - Show a single MeshTrace resource
* [kumactl get meshtraces](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshtraces)	 - Show MeshTrace
* [kumactl get meshtrafficpermission](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshtrafficpermission)	 - Show a single MeshTrafficPermission resource
* [kumactl get meshtrafficpermissions](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_meshtrafficpermissions)	 - Show MeshTrafficPermission
* [kumactl get proxytemplate](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_proxytemplate)	 - Show a single ProxyTemplate resource
* [kumactl get proxytemplates](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_proxytemplates)	 - Show ProxyTemplate
* [kumactl get rate-limit](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_rate-limit)	 - Show a single RateLimit resource
* [kumactl get rate-limits](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_rate-limits)	 - Show RateLimit
* [kumactl get retries](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_retries)	 - Show Retry
* [kumactl get retry](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_retry)	 - Show a single Retry resource
* [kumactl get secret](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_secret)	 - Show a single Secret resource
* [kumactl get secrets](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_secrets)	 - Show Secret
* [kumactl get timeout](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_timeout)	 - Show a single Timeout resource
* [kumactl get timeouts](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_timeouts)	 - Show Timeout
* [kumactl get traffic-log](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-log)	 - Show a single TrafficLog resource
* [kumactl get traffic-logs](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-logs)	 - Show TrafficLog
* [kumactl get traffic-permission](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-permission)	 - Show a single TrafficPermission resource
* [kumactl get traffic-permissions](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-permissions)	 - Show TrafficPermission
* [kumactl get traffic-route](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-route)	 - Show a single TrafficRoute resource
* [kumactl get traffic-routes](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-routes)	 - Show TrafficRoute
* [kumactl get traffic-trace](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-trace)	 - Show a single TrafficTrace resource
* [kumactl get traffic-traces](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_traffic-traces)	 - Show TrafficTrace
* [kumactl get virtual-outbound](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_virtual-outbound)	 - Show a single VirtualOutbound resource
* [kumactl get virtual-outbounds](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_virtual-outbounds)	 - Show VirtualOutbound
* [kumactl get zone](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_zone)	 - Show a single Zone resource
* [kumactl get zone-ingress](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_zone-ingress)	 - Show a single ZoneIngress resource
* [kumactl get zone-ingresses](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_zone-ingresses)	 - Show ZoneIngress
* [kumactl get zoneegress](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_zoneegress)	 - Show a single ZoneEgress resource
* [kumactl get zoneegresses](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_zoneegresses)	 - Show ZoneEgress
* [kumactl get zones](/docs/{{ page.release }}/generated/cmd/kumactl/kumactl_get_zones)	 - Show Zone

