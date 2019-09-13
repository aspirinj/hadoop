


```java
package spark.java.snippets;

import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import scala.Tuple2;

import java.util.Arrays;

public class WordCount{
    public static void main(String[] args) {
        SparkConf conf = new SparkConf().setAppName("JavaWordCount");
        JavaSparkContext jsc = new JavaSparkContext(conf);
        JavaRDD<String> lines = jsc.textFile("C:\\Users\\3627777\\Downloads\\spark\\data\\wc");
        JavaRDD<String> words = lines.flatMap(line -> Arrays.asList(line.split(" ")).iterator());
        JavaPairRDD<String, Integer> wordAndOne = words.mapToPair(w -> new Tuple2<>(w, 1));
        //聚合
        JavaPairRDD<String, Integer> reduced = wordAndOne.reduceByKey((m, n) -> m + n);
        //调整顺序
        JavaPairRDD<Integer, String> swaped = reduced.mapToPair(tp -> tp.swap());
        //排序
        JavaPairRDD<Integer, String> sorted = swaped.sortByKey(false);
        //调整顺序
        JavaPairRDD<String, Integer> result = sorted.mapToPair(tp -> tp.swap());
        //将结果保存到hdfs
        result.saveAsTextFile("C:\\Users\\3627777\\Downloads\\spark\\out");
        //释放资源
        jsc.stop();
    }
}


```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDYxODQ4NiwyMDQwMjk3NjIyXX0=
-->