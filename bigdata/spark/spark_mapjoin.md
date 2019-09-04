---
title: spark mapjoin
---

# Spark mapjoin使用方法

spark会自动识别表大小进行mapjoin，如果表小于10M就会broadcast

## 修改mapjoin配置

默认参数`spark.sql.autoBroadcastJoinThreshold=10485760`，即10M

## 使用Spark代码

```scala
spark.range(100).as("a")
  .join(broadcast(spark.range(100)).as("b"))
  .where($"a.id" === $"b.id")
```

## 执行Spark SQL，修改Hint

```sql
SELECT /*+ BROADCAST(r) */ * FROM records r JOIN src s ON r.key = s.key
```

# 注意

如果需要mapjoin的表是子查询，是无法mapjoin的，如下面的例子就无法广播

```sql
select *
from t_a a
join (...subquery...) b
    on a.key = b.key
```

被广播的表需要在hive中，或者被cache，关键是spark能否获取这个表的metadata（计算表大小）

## cache的方案

cache一个中间表

```sql
cache table t_b
select *
from ...
```

然后再mapjoin

```sql
select *
from t_a a
join t_b b
    on a.key = b.key
```

# 参考

https://spark.apache.org/docs/latest/sql-performance-tuning.html


