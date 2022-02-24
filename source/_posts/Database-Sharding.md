title: Database Sharding
date: 2021-03-14 23:28:42
tags:
---
Sharding is basically to break up your data across servers to improve the performance and/or infrastructure.

A replica set of MongoDB for example is replicating your data on any of your servers while sharding is breaking up the data across your servers. The process is called MongoS using Shard Key. When you connect and send queries to MongoDB, MongoS will look up the data and get it from the right place and also merge data if necessary because they can be on different servers.