![[Pasted image 20240618091349.png]]

The above picture demonstrates Spark API including: Spark SQL, Dataframe API, Dataset API. It highly recommend to use Spark SQl, Dataframes API instead of RDD APIs.

All of these APIs are powered by SQL Engine, a compiler, which optimizes your code to Java byte code runned on a JVM. 

![[Pasted image 20240618091915.png]]

There are 4 phase of Spark SQL operation. 

**1. Analysis:** In this phase, your code is analyzed, and the column names, table, or view names, SQL functions are resolved. You might get a runtime error shown as an analysis error at this stage when your names don't resolve.

**2. Logical Optimization:** SQL Enginer applies rule-based optimization and construct a set of multiple execution plans. The logical optimization includes standard SQL optimization techniques such as predicate pushdown, projection pruning, boolean expression simplification, and constant folding. The next phase is the physical planning the SQL engine picks the most effective logical plan.

**3.  Physical Planning:** this is a set of RDD operations, which determines how the plan is going to execute on Spark cluster

**4. Code Generation:** In the last phase, efficient Java bytecode is generated to run on each JVM 