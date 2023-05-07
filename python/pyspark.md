# Read and Write Files

## read

```python
df = sql_ctx.read \
    .option('header', 'true') \ # 是否有header（即列名）
    .option('inferschema', 'true') \ # 自动推断schema, 据我观察 这个操作会读两次文件
    .option('delimiter", ',') \
    .option('quote', '\"') \
    .csv('/tmp/csv_test')
```

## write

```python
df.write.mode('overwrite') \
    .option('header', 'true') \ # 是否有header（即列名）
    .option('ignoreLeadingWhiteSpace',False) \ # 是否去掉前的空白字符
    .option('ignoreTrailingWhiteSpace',False) \ # 是否去掉后面的空白字符
    .csv('/tmp/csv_test')
```

# Different Data Source

## redshift

```python
SPARK_REDSHIFT = (
    'jdbc:redshift://<url>'
    ':<port>/<schema>?user=<user>&password=<password>'
)
S3_TMP_DIR = '<s3_url>'

# sql query
sql = 'select * from <table> limit 10'
df = sql_ctx.read.format('com.databricks.spark.redshift') \
    .option('url', SPARK_REDSHIFT) \
    .option('query', sql) \
    .option('tempdir', S3_TMP_DIR) \
    .load()

# get data from table
df = sql_ctx.read.format('com.databricks.spark.redshift') \
    .option('url', SPARK_REDSHIFT) \
    .option('dbtable', table_name) \
    .option('tempdir', S3_TMP_DIR) \
    .load()

```

# Custom Pipeline

https://stackoverflow.com/questions/37270446/how-to-roll-a-custom-estimator-in-pyspark-mllib

```python
from pyspark.ml.pipeline import Estimator, Transformer
from pyspark.ml.param.shared import *
from pyspark.sql import functions as F

class HasK(Params):
    
    k = Param(Params._dummy(), 'k', 'k', TypeConverters.toInt)
    
    def __init__(self):
        super(HasK, self).__init__()
        
    def setK(self, value):
        return self._set(k=value)
    
    def getK(self):
        return self.getOrDefault(self.k)

class HasClusterCenters(Params):

    cluster_centers = Param(Params._dummy(), 'cluster_centers', 'cluster_centers', TypeConverters.toList)

    def __init__(self):
        super(HasClusterCenters, self).__init__()

    def setClusterCenters(self, value):
        return self._set(cluster_centers=value)

    def getClusterCenters(self):
        return self.getOrDefault(self.cluster_centers)

class OneClassKmeans(Estimator, HasFeaturesCol, HasPredictionCol, 
                     HasK, HasClusterCenters):
    def __init__(self, featuresCol="features", predictionCol="prediction", k=2,
                 initMode="k-means||", initSteps=2, tol=1e-4, maxIter=20, seed=None):
        super(OneClassKmeans, self).__init__()
        self.setFeaturesCol(featuresCol)
        self.setPredictionCol(predictionCol)
        self.setK(k)
    
    def _fit(self, dataset):
        x = self.getFeaturesCol()
        y = self.getPredictionCol()
        
        dataset.cache()
        dataset = dataset.withColumn(y, F.lit(0))
        
        udf_to_list = F.udf(lambda x: x.toArray().tolist(), ArrayType(FloatType()))
        dataset = dataset.withColumn(x, udf_to_list(x))
        
        # 计算中心
        n = len(dataset.select(x).first()[0])
        cc = dataset.groupBy(y) \
            .agg(F.array(*[F.avg(F.col(x)[i]) for i in range(n)]).alias('averages')) \
            .first()['averages']
        self.setClusterCenters(cc)
        
        dataset.unpersist()
        
        return (OneClassKmeansModel()
            .setFeaturesCol(self.getFeaturesCol())
            .setPredictionCol(self.getPredictionCol())
            .setK(self.getK())
            .setClusterCenters(self.getClusterCenters()))

class OneClassKmeansModel(Transformer, HasFeaturesCol, HasPredictionCol,
                          HasK, HasClusterCenters):
    def _transform(self, dataset):
        x = self.getFeaturesCol()
        y = self.getPredictionCol()
        return dataset.withColumn(y, F.lit(0))
    
    def clusterCenters(self):
        return self.getClusterCenters()
    
kmeans = OneClassKmeans(k=1, featuresCol='standardized_user_features', predictionCol='cluster_prediction')
kmeans
```

## 设置日志等级

```python
logger = sc._jvm.org.apache.log4j
logger.LogManager.getLogger("org").setLevel( logger.Level.ERROR )
logger.LogManager.getLogger("akka").setLevel( logger.Level.ERROR )
```