---
title: Create low-latency, multi-region apps with Kong Mesh and YugabyteDB
content_type: tutorial
description: This tutorial demonstrates how to build multi-region applications using Kong Mesh and YugabyteDB. This guide focuses on achieving low latency by deploying microservices in multiple cloud regions and using a distributed Postgres-compatible database.
---

This tutorial demonstrates how to build multi-region applications using {{site.mesh_product_name}} and a database, which is [YugabyteDB](https://www.yugabyte.com/) in this example. This guide focuses on achieving low latency by deploying microservices in multiple cloud regions and using a distributed Postgres-compatible database.

One reason multi-region applications are becoming more popular is because it can allow companies to achieve low latency for all users regardless of their region by creating identical applications that live in the same region as their users. In this tutorial, you've been tasked with deploying your company's clothing store app to multiple regions: New York in North America, Berlin in Europe, and Sydney in Australia. Your company wants the final app to handle read and write requests across all locations, which is why you choose to deploy the app in the regions where your customers are. This way, the app handles the requests with low latency, so your customers don't experience delays, especially during the busier shopping days during the year.

**overview of the steps involved**

## Architecture
what is in the demo app
what the services do
what is in each zone
Yugabyte as the DB, can use any
diagram of the thing

## Deploy a Geo-Partitioned Database Cluster
The first step in creating low-latency, multi-region apps with {{site.mesh_product_name}} is to deploy a database. In this guide, you'll be using YugabyteDB, but you can use any database of your choice.

YugabyteDB supports a geo-partitioned deployment mode which allows you to place user data in the three required locations. New York, Berlin, and Sydney. The fastest way to bootstrap a geo-partitioned cluster is by using YugabyteDB Managed:

Simply head to YugabyteDB Managed and initiate a dedicated partitioned cluster with nodes in N. Virginia (us-east4), Frankfurt (europe-west3), and Sydney (australia-southeast1).

Once the database is set up, execute the following script to create database objects used by the Kitchen and Tracker microservices. Among those database objects, the most noteworthy ones related to how the database utilizes the partitioning feature of Postgres to pin pizza orders to specific locations are: