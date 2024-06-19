
Firstly, notice that the data in spark is immutable

## 1.  Transformation
Transformations are operations on RDDs, DataFrames or Dataset thats produce a new distributed dataset from an existing one. They are generally lazy, meaning they are not executed immediately but immediately but create a logical execution plan. The transformations can cause shuffle, what can take more time than other methods.

**Examples of Transformations**: 
- ``map`` : applies a function to each element and produces a new DataFrame
- ``filter``: selects elements that satisfy a given condition
- ``groupBy``: same as SQL 
- ``join``: combines 2 datasets based on a common key
## 2. Actions
Actions are operations that trigger the execution of transformations and return a value to the driver program or write data to an external storage system. They are the operations that actually initiate the computation.

Different from transformation, **Actions** uses **eager evaluation**. Whenever variables generated, their values immediately are computed.

- ``collect``: retrieves all elements of the distributed dataset to the driver program
- ``count``: returns the number of elements in the distributed dataset

## 3. Functions
If a method is neither transformation nor action, it's a funtion. 