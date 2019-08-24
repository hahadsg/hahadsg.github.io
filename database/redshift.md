### epoch

* **epoch to date/time/datetime**
```sql
xxx : int
timestamp 'epoch' + xxx * interval '1 second'
```

* **date/time/datetime to epoch**
```sql
xxx : time/datetime/date
extract(epoch from xxx)
```

### 随机一个值 与 随机一批值
```sql
create temp table _zjf_tmp_test (i int, r int);
insert into _zjf_tmp_test (i,r) values (1,1), (2,2), (3,3), (4,4);
select * from _zjf_tmp_test order by i;
-- output: 1,1; 2,2; 3,3; 4,4

-- 随机一个值
update _zjf_tmp_test set r = (select random() * 100.0);
select * from _zjf_tmp_test order by i;
-- output: 1,17; 2,17; 3,17; 4,17

-- 随机一批值
update _zjf_tmp_test set r = random() * 100.0;
select * from _zjf_tmp_test order by i;
-- output: 1,11; 2,0; 3,37; 4,27
```

### S3

* s3 to redshift

```sql
COPY <table> 
FROM <s3_dir> 
credentials 'aws_access_key_id=<access>;aws_secret_access_key=<secret>' 
delimiter ',';
```

