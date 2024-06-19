RDD (Resilent Distributed Dataset) is a dataset , which similar to Dataframe (built on top of RDDs). However, unlike Dataframes, RDD records are just language-native objects and they do not have a row/column structure and a schema. So in simple words, RDD is just like a Scala, Java, or a Python collection.

a RDD Dataset is internally broken down into partitions to form a distributed collection. They are partitioned and spread across the executor cores  so they can be processed in parallel. RDDs are fault-tolerant because they also store infomation about how they are created. When an executor fails or crashes, the driver will assign the same RDD partition to another executor core. The new executor core will reload the RDD partition and start the processing. 

![[Pasted image 20240618095240.png]]

