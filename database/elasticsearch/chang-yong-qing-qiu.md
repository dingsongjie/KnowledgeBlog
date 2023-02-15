# 常用请求

### 获取集群健康状态

```bash
curl -u username:password localhost:9200/_cluster/health?pretty
```

### 集群索引未分配时获取集群分片计划

```bash
curl -u username:password localhost:9200/_cluster/allocation/explain?pretty

```

### 删除索引

```bash
curl -X DELETE -u admin:bestadmin localhost:9200/indexName

```

### 查看索引设置

```bash
curl -u username:password localhost:9200/indexName/_settings?pretty
```

### 修改索引设置

```bash
curl -X PUT -H 'Content-Type: application/json' -u username:password 'localhost:9200/indexName/_settings' -d  '{"index":{"routing":{"allocation":{"require._id":null}}}}'
```
