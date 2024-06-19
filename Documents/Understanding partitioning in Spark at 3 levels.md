There are 3 places

## 1) Input partitioning##

When loading data from a file, file system or directory.

Spark reads file in partitions and each partition is processed to reach the desired result. 

Depends mainly on 3 spark configurations:

<code>spark.sql.files.maxPartitionBytes</code>: The maximun number of bytes to pack into a single partition when reading files. Default value is set to 128MB.

<code>spark.sql.files.openCostInBytes</code> : The estimated cost to open a file. Default value is set to 4MB.

<code>spark.sparkContext.defaultParallelism</code>: Number of Cores available for Parallel operations.

## 2) Shuffle Partitions
Shuffle is a mechanism for redistributing or re-partitioning data so that is grouped differently across partitions. Shuffle partitions are partiions used at wide transformation. However, for wide transformations, the number of shuffle partitions is set to 200. It does not if your data is small or large, or if your cluster configuration has 20 executors, it is still 200.  

When working with varying data sizes in Spark, it's important to adjust the number of shuffl partitions.

There are 2 cases noticed:

**1. Few large partition**: problems of inefficient disk spills and out of memory errors in Executor.

**2. Many small partitions**: driver out of memory error as too many tasks created to carter the partitions and huge network overhead.

There are SparkSession's conf attribute to get and set dynamic Spark configuration properties.

```python
spark.conf.get("spark.sql.shuffle.partitions")
```

**3. Output partitioning**

How you write the output can significantly affect reading and retrieval of the necessary data in the future processing pipelines or data warehouse systems.

When writing a DataFrame to storage, the number of DataFrame partitions determines the number of data files written. (This assumes that Hive partitioning is not used for the data in storage)

As an example, consider a scenario where you have a sizable preprocessing cluster alongside a smaller, more budget-friendly service cluster. In this case, the recommended approach is to increase the number of partitions in the DataFrame before saving it. This ensures that the subsequent cluster will not face performance bottlenecks.

There are 2 methods available to repartition a DataFrame: **repartition** and **Coalesce**

**1) Repartion**

Returns a new Dataframe with has exactly n partitions. Wide transformation.

*Prospects:* evenly balances partition sizes
*Consequence:* requires shuffles all data

repartitonedDF = df.repartition(8)
repartitionDF.rdd.getNumPartitions()

**2)      Coalesce**

Returns a new DataFrame that has exactly n partitions, when fewer partitions are requested.

If a larger number of partitions is requested, it will stay at the current number of partitions.

Narrow transformation, some partitions are effectively concatenated

**Pro:** Requires no shuffling

**Cons:**

Is not able to increase # partitions

Can result in uneven partition sizes

**coalesceDF = df.coalesce(8)**

**coalesceDF.rdd.getNumPartitions()**


**In Conclusion,**

- if you are **increasing** the number of partitions use repartition()(_performing full shuffle_),
- if you are **decreasing** the number of partitions use coalesce() (_minimizes shuffles_)



