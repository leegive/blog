---
title: Elasticsearch聚合分析入门
date: 2019-01-13 15:48:00
tags: ElasticSearch
---

一些例子操作记录

<!-- more -->

## 计算商品每个tag下的商品数量

```
GET /ecommerce/product/_search
{
  "size": 0, 
  "aggs": {
    "group_by_tags": {
      "terms": {
        "field": "tags",
        "size": 10
      }
    }
  }
}
```

## 名称中包含yagao的商品，计算每个tag下的商品数量

先搜索后集合

```
GET /ecommerce/product/_search
{
  "size": 0, 
  "query": {
    "match": {
      "name": "yagao"
    }
  },
  "aggs": {
    "tags_group": {
      "terms": {
        "field": "tags",
        "size": 10
      }
    }
  }
}
```

## 计算每个tag下的商品的平均价格，并按照平均价降序

```
GET /ecommerce/product/_search
{
  "size": 0, 
  "aggs": {
    "terms_tags": {
      "terms": {
        "field": "tags",
        "order": {
          "avg_price": "desc"
        }
      },
      "aggs": {
        "avg_price": {
          "avg": {
            "field": "price"
          }
        }
      }
    }
  }
}
```

## 按照价格区间进行分组，然后再魅族内按照tag进行分组，再计算每组的平均价格

```
GET /ecommerce/product/_search
{
  "size": 0,
  "aggs": {
    "price_range": {
      "range": {
        "field": "price",
        "ranges": [
          {
            "from": 0,
            "to": 20
          },
          {
            "from": 20,
            "to": 40
          },
          {
            "from": 40,
            "to": 60
          }
        ]
      },
      "aggs": {
        "tags_terms": {
          "terms": {
            "field": "tags"
          },
          "aggs": {
            "avg_price": {
              "avg": {
                "field": "price"
              }
            }
          }
        }
      }
    }
  }
}
```
