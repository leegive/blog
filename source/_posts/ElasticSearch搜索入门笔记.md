---
title: ElasticSearch搜索入门笔记
date: 2019-01-13 14:58:43
tags: ElasticSearch
---

本篇目标是入门搜索联系，包括搜索全部商品，按售价排序，按部分商品名称搜索，或组合搜索排序等场景。

<!-- more -->

## 搜索全部商品

`GET /ecommerce/product/_search`

搜索结果的含义：

- took: 搜索时长，单位毫秒
- timed_out: 是否超时
- shards: 数据共多少个分片
- hits.total: 查询结果的数量
- hits.max_score: 搜索的相关度的匹配分数，越相关就越匹配，分数就越高
- hits.hits: 搜索结果

## 搜索商品名称包含yagao的商品，并且按照售价降序排序

```
GET /ecommerce/product/_search
{
  "query": {
    "match": {
      "name": "yagao"
    }
  },
  "sort": [
    {
      "price": {
        "order": "desc"
      }
    }
  ]
}
```

## 分页查询商品

```
GET /ecommerce/product/_search
{
  "query": {
    "match_all": {}
  },
  "from": 1,
  "size": 1
}
```

## 查询商品的名称和价格

```
GET /ecommerce/product/_search
{
  "query": {
    "match_all": {}
  },
  "_source": ["name", "price"]
}
```

## 搜索商品名称包含yagao,而且售价大于25的商品

```
GET /ecommerce/product/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "name": "yagao"
          }
        }
      ],
      "filter": {
        "range": {
          "price": {
            "gt": 25
          }
        }
      }
    }
  }
}
```

## 全文检索

全文检索，会分词查询文章，并计算匹配度相关分数,主要原理，参考倒排索引

```
GET /ecommerce/_search
{
  "query": {
    "match": {
      "producer": "yagao producer"
    }
  }
}
```

## 短语搜索 phrase search

跟全文检索相反，全文检索会将输入的搜索字符进行分词，然后去倒排索引里面去--匹配，只要能匹配上任意一个拆解后的词，就可以作为结果返回。而phrase search不进行分词，直接去倒排索引里面去匹配。

```
GET /ecommerce/_search
{
  "query": {
    "match_phrase": {
      "producer": "special yagao"
    }
  }
}
```

## 高粱显示

```
GET /ecommerce/product/_search
{
  "query": {
    "match": {
      "producer": "producer"
    }
  },
  "highlight": {
    "fields": {
      "producer": {}
    }
  }
}
```
