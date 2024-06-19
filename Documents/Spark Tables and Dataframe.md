## 1. Spark Tables and View
Spark is not only a set of APIs and a processing engine. But also, you can create databases and view using Spark. The table has 2 part: Table Data and Table Metadata. The table data still resides as data files in your distributed storage and the metadata hold the information about the table and its data such as schema, database name, column names, partitions and the physical location where the data actually resides. All of this is stored in a central meta-store called catalog. 

By default, Spark comes with an in-memory catalog which is maintained per spark session. However, this information goes away when the session ends. So, we needed a persistent and durable meta-store. Spark decided to reuse the Apache Hive meta-store. 

Spark allows to create 2 types of table: **managed table, unmanaged table**.

If you create managed tables, Spark do 2 things: ==create and store metadata in catalog== and ==write the data inside a predefined directory location (spark.sql.warehouse.dir)== 

To unmanaged tables, Spark give you the flexibility to store the data at your preferred location. 

``` sql
How to create umanaged table?

CREATE TABLE your_tbl_name(col1 datatype, col2 data_type,...)

USING PARQUET
LOCATION "data_file_location"
```

```sql
How to create managed table?

dataframe.write.saveAsTable("your_table_name")
```
