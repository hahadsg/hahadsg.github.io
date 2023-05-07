# Syntax

* Select Syntax
    
  https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Select
    
* Transform/Map-Reduce Syntax
  
  https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Transform
    
* regexp dict
  
  https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html
    
### create table and load data
  
```sql
create table {table} (
    col1 string
)
partitioned by (group_id string)
ROW format delimited
fields terminated by '\t'
STORED AS TEXTFILE;

load data local inpath '{path}' into table {table} partition(group_id='1');

```

### dynamic partition

自动根据day这列的值创建分区

```sql
SET hive.exec.dynamic.partition=true;  
SET hive.exec.dynamic.partition.mode=nonstrict; 
SET hive.exec.max.dynamic.partitions.pernode = 1000;
SET hive.exec.max.dynamic.partitions=1000;

insert overwrite table t_par partition (day)
select v1, v2, day from t_unpar;
```

### export data

* export with header

```sh
hive -e "set hive.cli.print.header=true; select * from table" > f.csv
```

### time type

* pattern参考

https://docs.oracle.com/javase/tutorial/i18n/format/simpleDateFormat.html

`u: day of week`

* convert

```sql
-- string to string
select from_unixtime(unix_timestamp('20181231', 'yyyyMMdd'), 'yyyy-MM-dd');

-- string to date
select to_date(from_unixtime(unix_timestamp('20181231', 'yyyyMMdd')));
```

### grouping sets

http://lxw1234.com/archives/2015/04/193.htm

### insert

```
-- insert overwrite partition
insert overwrite table test.test partition (day='20190114')
select col1, col2
from test.test2
```

# Advance hive

https://www.qubole.com/blog/hive-best-practices/

# Perference

### 高效抽样

```sql
-- 假设我们从1亿数据抽样100万
select *
from <table>
where rand() <= 0.05 -- 先大致淘汰大部分数据（剩下大约500万）
distribute by rand() -- 按rand()在每台机器上分布
sort by rand() -- 在每个reducer中sort
limit 1000000
```

# Trick

### 大量数据打上序号

```sql
-- test.table_origin中有大量数据，希望给其打上序号
-- 按proba降序排序 然后打上序号
-- 将proba分成1000组 分别rank 再合并
drop table if exists test.table_group;
create table test.table_group as
select id, proba, ceil(proba * 1000) as group_id
from test.table_origin
;
drop table if exists test.table_group_cumcount;
create table test.table_group_cumcount as
select group_id, cnt
    , sum(cnt) over(order by group_id rows between unbounded preceding and current row) as cum_cnt
from (
    select group_id, count(*) as cnt
    from test.table_group
    group by group_id
) t
;
drop table if exists test.table_temp_rank;
create table test.table_temp_rank as
select id, proba, group_id
    , row_number() over(partition by group_id order by proba desc) as group_rk
from test.table_group
;
drop table if exists test.table_rank;
create table test.table_rank as
select t1.id, t1.proba, t1.group_rk, t1.group_rk + t2.cum_cnt - t2.cnt as rk
from test.table_temp_rank t1
join test.table_group_cumcount t2
    on t2.group_id = t1.group_id
;

```