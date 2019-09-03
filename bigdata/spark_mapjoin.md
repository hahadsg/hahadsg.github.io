---
title: spark mapjoin
---

# Spark mapjoin

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

# 参考

https://spark.apache.org/docs/latest/sql-performance-tuning.html


