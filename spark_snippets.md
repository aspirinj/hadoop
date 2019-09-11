
### Setup



### Sample
```scala
import org.apache.spark.{SparkConf, SparkContext}  
  
object Test1 {  
  def main(args: Array[String]): Unit = {  
    val conf = new SparkConf().setAppName("Simple Spark").setMaster("local[2]")  
    val sc = new SparkContext(conf)  
    val rdd1 = sc.parallelize(List(1,2,3,4,5,6,7))  
    rdd1.saveAsTextFile("output")  
    sc.stop()  
  }  
}
```

### function
```scala
rdd.map(_*2)
rdd.map(x => x*2)  // equivalent
```




### Basics
```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val lines = a.filter(line => line.contains("Spark"))  // rows contains keywords
a.filter(line => line.contains("Spark")).count()  // row contains keywords count
```

Scala function literals (closures), `map`, `reduce`:
```scala
a.map(line => line.split(" ").size).reduce((a,b) => if (a>b) a else b)
import java.lang.Math                                               // equivalent
a.map(line => line.split(" ").size).reduce((a,b) => Math.max(a,b))  //equivalent
```

This first maps a line to an integer value, creating a new Dataset. `reduce` is called on that Dataset to find the largest word count. The arguments to `map` and `reduce` are Scala function literals (closures), and can use any language feature or Scala/Java library. For example, we can easily call functions declared elsewhere. 



### MapReduce
```scala
scala> val wordCounts = a.flatMap(line => line.split(" ")).groupByKey(identity).count()
```
Here, we call `flatMap` to transform a Dataset of lines to a Dataset of words, and then combine `groupByKey` and `count` to compute the per-word counts in the file as a Dataset of (String, Long) pairs. To collect the word counts in our shell, we can call `collect`:

```scala
scala> wordCounts.collect()
res6: Array[(String, Int)] = Array((means,1), (under,2), (this,3), (Because,1), (Python,2), (agree,1), (cluster.,1), ...)
```


### Caching
Spark also supports pulling data sets into a cluster-wide in-memory cache. This is very useful when data is accessed repeatedly, such as when querying a small “hot” dataset or when running an iterative algorithm like PageRank. As a simple example, let’s mark our `linesWithSpark` dataset to be cached:

```scala
scala> linesWithSpark.cache()
res7: linesWithSpark.type = [value: string]

scala> linesWithSpark.count()
res8: Long = 15

scala> linesWithSpark.count()
res9: Long = 15
```


### Self-Contained Applications
Suppose we wish to write a self-contained application using the Spark API. We will walk through a simple application in Scala (with sbt), Java (with Maven), and Python (pip).

We’ll create a very simple Spark application in Scala–so simple, in fact, that it’s named `SimpleApp.scala`:

```scala
/* SimpleApp.scala */
import org.apache.spark.sql.SparkSession

object SimpleApp {
  def main(args: Array[String]) {
    val logFile = "YOUR_SPARK_HOME/README.md" // Should be some file on your system
    val spark = SparkSession.builder.appName("Simple Application").getOrCreate()
    val logData = spark.read.textFile(logFile).cache()
    val numAs = logData.filter(line => line.contains("a")).count()
    val numBs = logData.filter(line => line.contains("b")).count()
    println(s"Lines with a: $numAs, Lines with b: $numBs")
    spark.stop()
  }
}
```

Note that applications should define a `main()` method instead of extending `scala.App`. Subclasses of `scala.App` may not work correctly.

This program just counts the number of lines containing ‘a’ and the number containing ‘b’ in the Spark README. Note that you’ll need to replace YOUR_SPARK_HOME with the location where Spark is installed. Unlike the earlier examples with the Spark shell, which initializes its own SparkSession, we initialize a SparkSession as part of the program.

We call `SparkSession.builder` to construct a [[SparkSession]], then set the application name, and finally call `getOrCreate` to get the [[SparkSession]] instance.

Our application depends on the Spark API, so we’ll also include an sbt configuration file, `build.sbt`, which explains that Spark is a dependency. This file also adds a repository that Spark depends on:

```scala
name := "Simple Project"

version := "1.0"

scalaVersion := "2.12.8"

libraryDependencies += "org.apache.spark" %% "spark-sql" % "2.4.4"
```

For sbt to work correctly, we’ll need to layout `SimpleApp.scala` and `build.sbt` according to the typical directory structure. Once that is in place, we can create a JAR package containing the application’s code, then use the `spark-submit` script to run our program.

```bash
# Your directory layout should look like this
$ find .
.
./build.sbt
./src
./src/main
./src/main/scala
./src/main/scala/SimpleApp.scala

# Package a jar containing your application
$ sbt package
...
[info] Packaging {..}/{..}/target/scala-2.12/simple-project_2.12-1.0.jar

# Use spark-submit to run your application
$ YOUR_SPARK_HOME/bin/spark-submit \
  --class "SimpleApp" \
  --master local[4] \
  target/scala-2.12/simple-project_2.12-1.0.jar
...
Lines with a: 46, Lines with b: 23
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUyODkyODgzNCwyMDU4MDg5MjA4LDcyND
cwOTY4OSwtMzQzNTE2MjIzLDE4MDAwOTcwNjAsOTkyNDAwMTg2
LDEyMzgyMTUzNDYsMjA3MTYzOTg1NSw3NDAxODE2NjMsMTAzND
Q1ODIwMiwtOTgxMzEzNjYwXX0=
-->