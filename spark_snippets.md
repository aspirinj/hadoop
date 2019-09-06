

```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val linesWithSpark = a.filter(line => line.contains("Spark"))  // rows contains keywords
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAzNDQ1ODIwMiwtOTgxMzEzNjYwXX0=
-->