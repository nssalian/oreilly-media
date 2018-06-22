# Cluster Managers in Spark

## For MESOS


### Setting up

To use Mesos from Spark, you need a Spark binary package available in a place accessible by Mesos, 
and a Spark driver program configured to connect to Mesos.

Alternatively, you can also install Spark in the same location in all the Mesos slaves, 
and configure `spark.mesos.executor.home` (defaults to `SPARK_HOME`) to point to that location.


### Uploading Jar

The slave running Mesos must have a Spark binary package for running the Spark Mesos executor backend.

To host on HDFS, use the Hadoop fs put command: 

`hadoop fs -put spark-2.3.1.tgz /path/to/spark-2.3.1.tgz`
### In Client Mode

In client mode, a Spark Mesos framework is launched directly on the client machine and waits for the driver output.

The driver needs some configuration in spark-env.sh to interact properly with Mesos:

In spark-env.sh set some environment variables:
```
export MESOS_NATIVE_JAVA_LIBRARY=<path to libmesos.so>. 
This path is typically <prefix>/lib/libmesos.so where the prefix is /usr/local by default. 
On Mac OS X, the library is called libmesos.dylib instead of libmesos.so.

export SPARK_EXECUTOR_URI=<URL of spark-2.3.1.tgz uploaded above>.
Also set spark.executor.uri to <URL of spark-2.3.1.tgz>.

```


```
val conf = new SparkConf()
  .setMaster("mesos://HOST:5050")
  .setAppName("My app")
  .set("spark.executor.uri", "<path to spark-2.3.1.tgz uploaded above>")
val sc = new SparkContext(conf)

```

### In Cluster Mode

Spark on Mesos also supports cluster mode, where the driver is launched in the cluster and the client can find 
the results of the driver from the Mesos Web UI.

To use cluster mode, you must start the `MesosClusterDispatcher` in your cluster via the `sbin/start-mesos-dispatcher.sh` script, 
passing in the Mesos master URL (e.g: `mesos://host:5050`). This starts the `MesosClusterDispatcher` as a daemon running on the host.


### Spark Submit Command
```
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master mesos://<ip_address>:<port> \
  --deploy-mode cluster \
  --executor-memory 2G \
  --total-executor-cores 10 \
  http://path/to/examples.jar \
  1000
```  


For More Details and Configurations: `http://spark.apache.org/docs/latest/running-on-mesos.html`