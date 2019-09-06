
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

It may seem silly to use Spark to explore and cache a 100-line text file. The interesting part is that these same functions can be used on very large data sets, even when they are striped across tens or hundreds of nodes. You can also do this interactively by connecting `bin/spark-shell` to a cluster, as described in the [RDD programming guide](https://spark.apache.org/docs/latest/rdd-programming-guide.html#using-the-shell).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExMTQ2NDY3NywxODAwMDk3MDYwLDk5Mj
QwMDE4NiwxMjM4MjE1MzQ2LDIwNzE2Mzk4NTUsNzQwMTgxNjYz
LDEwMzQ0NTgyMDIsLTk4MTMxMzY2MF19
-->