
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxMDU4NDc4Niw5OTI0MDAxODYsMTIzOD
IxNTM0NiwyMDcxNjM5ODU1LDc0MDE4MTY2MywxMDM0NDU4MjAy
LC05ODEzMTM2NjBdfQ==
-->