### jupyter notebook

https://blog.csdn.net/sinat_27634939/article/details/80146340

### build project on the command line

https://docs.scala-lang.org/getting-started-sbt-track/getting-started-with-scala-and-sbt-on-the-command-line.html

## SBT
---

### common cmd

  ```
  // 单次compile
  compile
  // 单次run
  run
  // 单次test
  test
  // 持续run（只要文件修改就run）
  ~run
  ```

## 技巧

### argmax

```scala
scala> List(3,5,2,8).view.zipWithIndex.maxBy(_._1)._2
res1: Int = 3

scala> List(3,5,2,8).view.zipWithIndex.maxBy(_._1)
res2: (Int, Int) = (8,3)
```


