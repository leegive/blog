---
title: ElasticSearch笔记
date: 2019-01-13 10:27:35
tags: ElasticSearch
---

ElasticSearch基础操作,入门学习笔记。

<!-- more -->

## 集群管理基础命令

**快速检查集群的健康状况**

`GET /_cat/health?v`

**查看所有的索引信息**

`GET _cat/indices?v`

**创建索引**

`PUT /test_index_two?pretty`

**删除索引**

`DELETE /test_index_two`

## 商品CRUD

### 增加商品

```
PUT /ecommerce/product/1
{
    "name": "gaolujie yagao",
    "desc": "gaoxiao meibai",
    "price": 30,
    "producer": "gaolujie producer",
    "tags": ["meibai", "fangzhu"]
}

PUT /ecommerce/product/2
{
    "name": "jiajieshi yagao",
    "desc": "youxiao fangzhu",
    "price": 25,
    "producer": "jiajieshi producer",
    "tags": ["fangzhu"]
}

PUT /ecommerce/product/3
{
    "name": "zhonghua yagao",
    "desc": "caoben zhiwu",
    "price": 40,
    "producer": "zhonnghua producer",
    "tags": ["qingxin"]
}
```

> ES 会自动创建index,type，默认会对每个field都建立倒排索引。

### 查询商品

```
GET /ecommerce/product/1
```

### 修改商品，替换商品

```
PUT /ecommerce/product/1
{
    "name": "jiaqiangbenn gaolujie yagao",
    "desc": "gaoxiao meibai",
    "price": 30,
    "producer": "gaolujie producer",
    "tags": ["meibai", "fangzhu"]
}
```

### 修改商品, 更新商品

```
POST /ecommerce/product/1/_update
{
  "doc": {
    "name": "gaolujie yagao"
  }
}
```

### 删除商品

```
DELETE /ecommerce/product/1
```