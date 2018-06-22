# Cluster Managers in Spark


## For Standalone

### For Master

`./sbin/start-master.sh`

Once started, the master will print out a spark://HOST:PORT URL for itself, 
which you can use to connect workers to it

### For Slave 

`./sbin/start-slave.sh <master-spark-URL>`

Obtain the URL above and place it here

Look for more scripts in the /sbin directory 

### To run an application on the Spark cluster

Simply pass the spark://IP:PORT URL of the master as to the SparkContext constructor.
    
To run an interactive Spark shell against the cluster, run the following command:
    
`./bin/spark-shell --master spark://IP:PORT`

### Resource Scheduling

The standalone cluster mode currently only supports a simple FIFO scheduler across applications

```
val conf = new SparkConf()
  .setMaster(...)
  .setAppName(...)
  .set("spark.cores.max", "10")
val sc = new SparkContext(conf)
```


Additional Details can be found here: `http://spark.apache.org/docs/latest/spark-standalone.html`
