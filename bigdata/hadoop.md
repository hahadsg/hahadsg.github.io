## 开启hdfs

```bash
# hdfs
/opt/hadoop-2.7.4/bin/hdfs namenode -format
/opt/hadoop-2.7.4/sbin/start-dfs.sh
```

# 问题

## hadoop fs -ls报错ls: ‘.’: No such file or directory

```
# 需要先创建home:/user/<user>
hadoop fs -mkdir -p /user
hadoop fs -mkdir -p /user/hahadsg
```