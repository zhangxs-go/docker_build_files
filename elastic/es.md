### 创建索引映射(mapping)
```json
PUT /product-pool
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text"
      }
    }
  }
}
```

### 增加别名
```json
POST /_aliases
{
  "actions": [
    {
      "add": {
        "index": "my-data-stream",
        "alias": "my-alias"
      }
    }
  ]
}
```

### 创建一个管道处理pipeline
```json 
PUT _ingest/pipeline/my_timestamp
{
  "description": "添加创建时间",
  "processors": [
    {
      "set": {
        "field": "created_at",
        "value": "{{_ingest.timestamp}}"
      }
    }
  ]
}
```

### 聚合查询
```json 
PUT _ingest/pipeline/my_timestamp
{
  "size": 0,
  "query": {
    "term": {
      "status": {
        "value": "OnSelling"
      }
    }
  }, 
  "aggs": {
    "category_product_num": {
        "terms": {
            "field": "parent_category_id.keyword",
            "include": [],
            "order": {
                "_count": "desc"
            },
            "size": 14
        }
    }
  }
}
```