设计、介绍：https://kafka.apache.org/intro#kafka_mq

# 参数
-----

### auto.offset.reset

* earliest

  当各分区下有已提交的offset时，从提交的offset开始消费；无提交的offset时，从头开始消费
  
* latest 
  
  当各分区下有已提交的offset时，从提交的offset开始消费；无提交的offset时，消费新产生的该分区下的数据 

* none 

  topic各分区都存在已提交的offset时，从offset后开始消费；只要有一个分区不存在已提交的offset，则抛出异常
  
# Spark Streaming + Kafka
-----

### 不丢失数据

  http://aseigneurin.github.io/2016/05/07/spark-kafka-achieving-zero-data-loss.html
  
几种方法对比：

https://spark.apache.org/docs/2.2.0/streaming-kafka-0-10-integration.html

* checkpoint

  使用sparkstreaming自带的checkpoint机制，不仅能够保证offset被记录下来，而且spark出错也能够恢复，不过数据处理要保证幂等性；缺点是checkpoint需要保存在hdfs等永久存在的文件系统上，性能上会差一些，另外，如果代码修改了，checkpoint就失效了
  
* kafka自带的commit

  先执行完处理，然后commit，同样需要保证output的幂等性，个人认为这个方法最好，但是只有sparkstreaming-kafka-0.10后才支持，而且还没有python版本
  
* 自己保存offset

  实质跟上面的方法没有区别，只是自己来做

# 参考
-----

http://www.infoq.com/cn/articles/kafka-analysis-part-1