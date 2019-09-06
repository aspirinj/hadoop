

```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val lines = a.filter(line => line.contains("Spark"))  // rows contains keywords
a.filter(line => line.contains("Spark")).count()  // row contains keywords count
a.map(line => line.split(" ").size).reduce((a,b) 
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NzAxNTg0NzIsNzQwMTgxNjYzLDEwMz
Q0NTgyMDIsLTk4MTMxMzY2MF19
-->