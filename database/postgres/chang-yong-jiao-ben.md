# 常用脚本

### 登陆

```bash
psql -U <username> -W  <dbname>
```

### 查看所有的数据库

```sql
select datname from pg_database;
```

### 查看所有的表

```sql
SELECT table_name FROM information_schema.tables WHERE table_schema = <schema-name>;
```

### 查看表的列组成

```sql
SELECT column_name FROM information_schema.columns WHERE table_name =<table-name>;
```

### 创建表

```sql
CREATE TABLE cities (
        name     varchar(80) primary key,
        location point
);

CREATE TABLE weather (
        city      varchar(80) references cities(name),
        temp_lo   int,
        temp_hi   int,
        prcp      real,
        date      date
);
```

### 插入数据

```sql
INSERT INTO weather VALUES ('Berkeley', 45, 53, 0.0, '1994-11-28');

```

### 事务

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100.00
    WHERE name = 'Alice';
-- etc etc
COMMIT;


BEGIN;
UPDATE accounts SET balance = balance - 100.00
    WHERE name = 'Alice';
-- etc etc
ROLLBACK;
```
