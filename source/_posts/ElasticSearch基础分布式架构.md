---
title: ElasticSearch基础分布式架构
date: 2019-01-13 16:37:51
tags: ElasticSearch
---

1. ElasticSearch对复杂分布式机制的透明隐藏特性
2. ElasticSearch的垂直扩容与水平扩容
3. 增加减少节点的数据rebalance
4. master节点
5. 节点平等的分布式架构

<!-- more -->

# ElasticSearch对复杂分布式机制的透明隐藏特性

ElasticSearch是分布式架构。隐藏了复杂的分布式机制：

- 分片机制
- cluster discovery
- shard负载均衡
- shard副本
- 请求路由
- 集群扩容
- shard重分配


