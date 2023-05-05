# 常用脚本



### 查看指定数据库表表空间

```sql

SELECT 
    table_schema AS `Database`, 
    table_name AS `Table`, 
    CONCAT(ROUND(((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024 / 1024), 2), 'GB') AS `used`,
		CONCAT(ROUND(((DATA_FREE ) / 1024 / 1024 / 1024), 2), 'GB') AS `Free`
FROM 
    information_schema.TABLES 
WHERE 
    table_schema = '<db_name>' AND table_name = '<table_name>';
		
```

### 查看数据库内所有表的表空间信息

```sql
SHOW TABLE STATUS
```

### 优化表空间和索引等碎片

```sql
OPTIMIZE TABLE <table_name>

```

### 直接清楚表里的所有数据并压缩表空间

```sql
TRUNCATE TABLE <table_name>
```
