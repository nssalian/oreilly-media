# Cluster Managers in Spark

## YARN

### Launching YARN

Launching Spark on YARN
Ensure that `HADOOP_CONF_DIR` or `YARN_CONF_DIR` points to the directory which contains the (client side) configuration files
for the Hadoop cluster. These configs are used to write to HDFS and connect to the YARN ResourceManager. 
The configuration contained in this directory will be distributed to the YARN cluster so that all containers used by the application
use the same configuration. 

### Spark Application 

To launch a Spark application in cluster mode:

```
$ ./bin/spark-submit --class path.to.your.Class 
--master yarn 
--deploy-mode cluster [options] <app jar> [app options]
```
To launch a Spark application in client mode:

```
$ ./bin/spark-submit --class path.to.your.Class 

--master yarn 

--deploy-mode client [options] <app jar> [app options]
```

The above starts a YARN client program which starts the default Application Master. 

Then SparkPi will be run as a child thread of Application Master. 

More Details can be found here `http://spark.apache.org/docs/latest/running-on-yarn.html`
