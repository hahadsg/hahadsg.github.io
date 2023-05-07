# System table
-----

* 正在执行的sql

```sql
select *
from pg_stat_activity
order by query_start desc
```