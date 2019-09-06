

```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val lines = a.filter(line => line.contains("Spark"))  // rows contains keywords
a.filter(line => line.contains("Spark")).count()  // row contains keywords count
a.map(line => line.split(" ").size).reduce((a,b) => if (a>b) a else b)
a.map(line => line.split(" ").size).reduce((a,b) => Math.max(a,b))
```

This first maps a line to an integer value, creating a new Dataset. `reduce` is called on that Dataset to find the largest word count. The arguments to `map` and `reduce` are Scala function literals (closures), and can use any language feature or Scala/Java library. For example, we can easily call functions declared elsewhere. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU2NjkzMDU3OCwyMDcxNjM5ODU1LDc0MD
E4MTY2MywxMDM0NDU4MjAyLC05ODEzMTM2NjBdfQ==
-->