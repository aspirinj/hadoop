

```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val lines = a.filter(line => line.contains("Spark"))  // rows contains keywords
a.filter(line => line.contains("Spark")).count()  // row contains keywords count
```



This first maps a line to an integer value, creating a new Dataset. `reduce` is called on that Dataset to find the largest word count. The arguments to `map` and `reduce` are Scala function literals (closures), and can use any language feature or Scala/Java library. For example, we can easily call functions declared elsewhere. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyOTYyNjQ2MDEsMjA3MTYzOTg1NSw3ND
AxODE2NjMsMTAzNDQ1ODIwMiwtOTgxMzEzNjYwXX0=
-->