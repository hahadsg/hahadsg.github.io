# 参考
-----
优化表设计：https://docs.aws.amazon.com/zh_cn/redshift/latest/dg/tutorial-tuning-tables.html

# system table
-----

* 查看锁表情况

```sql
select *
from admin.v_check_transaction_locks
where granted='true'
```

* 杀掉进程

```sql
select pg_terminate_backend(28520)
```

* 查看load_error（S3 to redshift）

```sql
select *
from stl_load_errors
order by starttime desc
limit 10
```

* 查看表大小

```sql
select "schema", "table", "size", "tbl_rows"
from SVV_TABLE_INFO
order by "size" desc
limit 100
```

* 查看列默认值

```sql
select *
from "INFORMATION_SCHEMA"."COLUMNS"
where table_schema = 'schema' and "table_name" = 'table'
```

# syntax
-----

### create user

```sql
-- 创建、删除用户
create user guest password 'ABCd4321';
drop user guest;
-- 把用户添加进组
create group adminguest;
alter group adminguest add user guest;

-- 给表权限 USAGE必须给
GRANT USAGE ON SCHEMA public TO guest;
GRANT UPDATE, SELECT, INSERT, DELETE, REFERENCES ON ALL TABLES IN SCHEMA public TO guest;
```

### grant

```sql
grant update, select, insert, delete, references
on [table]
to group dc_user
```

### epoch

```sql
-- date/time/datetime to epoch
timestamp 'epoch' + [interval::int] * interval '1 second'
-- epoch to date/time/datetime
extract(epoch from [dt::datetime/time/date])
```