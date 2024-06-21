![[/images/Spark_Read_Operation.png]]

A file is stored in S3 or HDFS (specified distributed storages). Assume that you have these 10 nodes storage cluster in HDFS. The .csv file can be broken into many smaller partitions and stored in these 10 nodes. Since the file is partitioned, so the DataFrameReader is also going to read them as a bunch of in-memory partitions.

When you call a **DataFrameReader** means you have requested SparkSession as a spark driver to load all partitions of file. At runtime, your driver knows how to read the data and how many partitions are there and create a logical in-memory structure. But notice that there are nothing loaded, it only represents logical with enough information to load data. You can think your DataFrame as a bunch of smaller DataFrame each logically representing a partition. Spark do not actually load these data until an action is called on this Dataframe (I think this is reasonable to use logical in-memory for loading).

Then, the driver reaches out the cluster manager and asks for containers. In this case, each executor JVM is started with 5 CPU cores and 10GB memory. So, the driver is going to assign some DataFrame partitions to each JVM core. Moreover, when loading data, the driver is going to allocate the executors which is the closest to the partitions in the network. This is how the spark optimizes the bandwidth. 
