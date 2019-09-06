

```scala
val a = spark.read.textFile("a.txt")
a.count()  // total row count
a.first()  // first row content
val lines = a.filter(line => line.contains("Spark"))  // rows contains keywords
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAxMzMwMTUwMywxMDM0NDU4MjAyLC05OD
EzMTM2NjBdfQ==
-->