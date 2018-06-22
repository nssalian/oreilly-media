# Running Spark Application on YARN

## Setup

We have seen the Installing Spark; refer [Installation Document](spark-playbook/video 1/Setup.md)

Upon getting the setup done on the machine we need to make sure Spark and Hadoop, in this case,
YARN.

Primarily you need to make sure the `HADOOP_CONF_DIR` or the `YARN_CONF_DIR` is set correctly to point 
to your local installation's configuration.


## Running the Application

Once that is done, you can run the application you intend with the following command specifying the 
jar file and the class you wish to execute in it.

So, here we execute the WordCount class in the examples jar for Spark that comes built in.
```
 spark-submit 
 --class org.apache.spark.examples.SparkPi 
 --deploy-mode cluster 
 --master yarn 
 /usr/lib/spark/lib/spark-examples.jar 
 10
```

