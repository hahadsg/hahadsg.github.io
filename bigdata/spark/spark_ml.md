## get features vector name

https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/5211178207246023/3527163800997788/7788830288800223/latest.html

```scala
import org.apache.spark.ml.attribute._
import org.apache.spark.ml.feature._

case class Person(name: String, age: Integer, gender: Integer)
val personSeq = Seq(
  Person("name1", 22, 0),
  Person("name2", 30, 1)
)
val df = personSeq.toDF()

val assembler = new VectorAssembler()
  .setInputCols(Array("age", "gender"))
  .setOutputCol("features")
val transformedDF = assembler.transform(df)

val schema = transformedDF.schema
val featureAttrs = AttributeGroup.fromStructField(schema("features")).attributes.get
val features = featureAttrs.map(_.name.get)

```

## 强制设置模型参数

如果想使用LR的参数直接生成一个model，可以先new一个LogisticRegressionModel，然后再强制set他的参数

```scala
// create model with coeff
val lrModel = new LogisticRegressionModel(uid, coefficientMatrix, interceptVector, numClasses, isMultinomial)
// set param
lrModel.set(lrModel.regParam, 0.1)
```

