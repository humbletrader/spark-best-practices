# spark-best-practices
List of best practices and fixes for issues encountered while developing spark applications and their 

# Getting information about the issue
* Check the log of the application
  * Disk full
  * OutOfMemory
  * Timeout

* Check the Spark console
  * size of variables
  * size of persisted RDDs
  * free / available memory for storage

* Check the Hadoop console for dead nodes

* Check Ganglia reports

* Check CloudWatch

# Solving the issues discovered
 ## solving OOM issues
  * there’s no generic rule but most of the OOM issues
  * unpersist broadcasted variables as soon as possible ( sync if hot )
  * use Iterators when possible ( avoid multiple maps when non iterators as they pollute the eden)
  * in hot areas we should use primitives instead of java classes
  * detect memory size of your structure
  * avoid as much as possible transfers from java to scala structures and viceversa
  * avoid heavy-on-memory documented rdd operations ( groupBy )
  * take control of your memory settings
    * control your driver and executor heap
    * be aware of your executor overhead and/or control it
  * don't go over 32 GB / executor 

 ## solving disk full issues
  * check the size of your persisted data ( spark ui )
  * kryo & gzip
  * make sure you don’t log too much ( i.e opportunities )

 ## solving runtime performance issues
  * Kryo serialization
  * persist when re-using RDDs 
  * Combine multiple RDD.maps/flatMaps/filters into one single RDD.map operation if possible
  * check CPU hotspots with a profiler

 
