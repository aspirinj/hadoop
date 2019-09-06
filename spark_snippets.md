

```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val lines = a.filter(line => line.contains("Spark"))  // rows contains keywords
a.filter(line => line.contains("Spark")).count()  // row contains keywords count
a.map(line => line.split(" ").size).reduce((a,b) => if (a>b) a else b)
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3MTYzOTg1NSw3NDAxODE2NjMsMTAzND
Q1ODIwMiwtOTgxMzEzNjYwXX0=
-->