[Quick-Start](https://spark.apache.org/docs/latest/quick-start.html)
```java
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.SparkSession;

import static org.apache.spark.sql.functions.col;

public class SimpleApp {
    public static void main(String[] args) {
        String logFile = "/Users/qinshunong1/spark-3.3.0-bin-hadoop3/README.md";
        SparkSession sparkSession = SparkSession.builder().appName("Simple Application").config("spark.master","local").getOrCreate();
        Dataset<String> logData = sparkSession.read().textFile(logFile).cache();

        long numAs = logData.count();
//        long numBs = logData.filter(s -> s.contains("b")).count();
        long numBs = logData.filter(col("value").contains("b")).count();
        System.out.println("Lines with a: " + numAs + ", lines with b: "+numBs);


        sparkSession.stop();
    }
}
```