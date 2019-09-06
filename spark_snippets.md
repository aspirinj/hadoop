

```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val lines = a.filter(line => line.contains("Spark"))  // rows contains keywords
a.filter(line => line.contains("Spark")).count()  // row contains keywords count
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQwMTgxNjYzLDEwMzQ0NTgyMDIsLTk4MT
MxMzY2MF19
-->