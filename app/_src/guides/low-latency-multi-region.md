---
title: Create low-latency, multi-region apps with Kong Mesh and YugabyteDB
content_type: tutorial
description: This tutorial demonstrates how to build multi-region applications using Kong Mesh and YugabyteDB. This guide focuses on achieving low latency by deploying microservices in multiple cloud regions and using a distributed Postgres-compatible database.
---

This tutorial demonstrates how to build multi-region applications using {{site.mesh_product_name}} and a database, which is [YugabyteDB](https://www.yugabyte.com/) in this example. This guide focuses on achieving low latency by deploying microservices in multiple cloud regions and using a distributed Postgres-compatible database.

One reason multi-region applications are becoming more popular is because it can allow companies to achieve low latency for all users regardless of their region by creating identical applications that live in the same region as their users. In this tutorial, you've been tasked with deploying your company's clothing store app to multiple regions: New York in North America, Berlin in Europe, and Sydney in Australia. Your company wants the final app to handle read and write requests across all locations, which is why you choose to deploy the app in the regions where your customers are. This way, the app handles the requests with low latency, so your customers don't experience delays, especially during the busier shopping days during the year.

## Architecture
