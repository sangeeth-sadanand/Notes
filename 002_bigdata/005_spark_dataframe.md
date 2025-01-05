# Sparks API- Dataframe and SQL

- RDD does not have any structure
- It is raw data which is distributed accross various partitions
- There is no schema or metadata 
- Spark SQL or table is persistant over a session. Data files are stored on the disk (any storage like the HDFS/S3) and metastore/ schema is stored on metastore.
- Dataframes are form of RDDs with some stucture/ schema that is not persistant as it is avalable only in perticular session. Data is stored in memory and metastore is saved in a temporary location.
- The higher level API's is more performant because of the spark engine is provided with more context to handle data effectively with the help of meta data information.

## Working with Dataframes

1. Load the data file and create dataframe
2. Apply transformation
3. Write result back to storage

## Read operation

```python
spark.read\
.format( "csv" )\
.option(" header"," true" ).
.option (" infer Schema"," true")\
.load( "path")
```

- It is not recommended to infer schema
  
  - It may not infer the schema correctly
  - It can lead to preformance issues as spark scans the data in order to determine the schema

- SQL table to data frame & vise a versa
  
  - **createOrReplaceTempView** :- creates a table if table exist then it replaces the table without throwing error.
  - **createTempView**:- creates a table if table exists, then it throws error stating table already exists.
  - **createGlobalTempView**:- the table view will be  visible across other applications as well
  - **createOrReplaceGlobalTempView**:- replace any existing table  view with newly created table.

## Creating a Spark table:-

- If a table is created without selecting the database in which it has to be created. it will be created under default database

```python
spark.sql(" create databases if not exists a <database-name>")
```

## To View the database

```python
spark.Sql("show databases")
```

- To view databases with certain pattern

```python
spark.sql("show databases").filter( "name like <name>") 
```

## To view table

```sql
show tables
```

## Describe extended table

```sql
Describe extended "<table_name>"
```

## Types of table

1. External
2. Managed

### External

- The data is already present in a specific location and a structure has
  to be created to get a tabular view
- When a data is dropped only the meta data is lost

### Managed

- Create an empty table
- Load the data from a temporary table
- When the table is dropped, both the data & metadata is lost.

### Managed Vs External table

- When the data is owned by a single user then managed tables could be used.
- If multiple users are accessing the data kept at a centralised location.
- Then it is best to use external table insert & select can only be used.

## Spark optimization & tuning

1. Code level optimization
2. Cluster level optimization

### Resource level optimization

- In order for a job to run effectively the right amount of resources should be allocated.
- Resource include:
  - Memory (RAM)
  - CPU cores (compute)

### Strategies for creating clusters

- Thin Executors
  
  - More executors created holding minimal resource.
  
  - each executor will hold CPU core & Machine RAM/ No of executor.
  
  - Drawbacks
    
    - No multi-threading
    - Shared variables leads to multiple copies

- Fat Executors
  
  - Give copies maximum leads resource to each executors.
  - 1 executor for a machine.
  - Drawbacks
    - HDFS troughput suffers
    - Takes a lot of time for garbage collector

### Best strategies

- A balance approach is the best stratagies
- Overhead / offheap Memory = max(384 MB, 7% of executor memory)

## Schema inference challenges

- Inferring schema is not the best choice

- It could lead to incorrect schema inference

- Spark has to scan the data to infer the schema which is time consuming and burdens the system there by affecting the performance

> Note: Schema should be enforced and not inferred.

**Sampling ratio** Instead of scanning the entire dataset, inferring the schema based on the ratio provided.

Two ways to enforce schema 

1. **Schema option - Schema DDL**
   
   ```python
   order_schema = 'order_id long, order_date date cust_id long, order_status string'
   ```
   
   df = (
   
       spark.read
       .format("csv")
       .schema(order_schema)
       .load()
   
   )

```
2. **StructType**

```python
from pyspark.sql.types import *


order_schema = StructType([
    StructField("order_id", LongType()),
    StructField("order_date", DateType()),
    StructField("cust_id", IntegerType()),
    StructField("order_status", StringType()),
])


df = (
    spark.read
    .format("csv")
    .schema(order_schema)
    .load()
)
```

3. **Nested Schema**
   
   1. SQL schema approach
      
      ```python
      ddlSchema = "customer_id long,"
              "fullname struct<firstname:string,lastname:string>,"
              "city string"
      ```
      
      df= (
      
          spark.read.format("json")
          .schema(ddlSchema)
          .load("/public/trendytech/datasets/customer_nested/*")
      
      )
      
      ```
      
      ```

4. Sruct type
   
   ```python
   customer_schema = StructType([
               StructField("customer_id",LongType()),
               StructField("fullname",
                   StructType([
                   StructField("firstname",StringType()),
                   StructField("lastname",StringType())
               ])),
               StructField("city",StringType())
           ])
   df= (
       spark.read.format("json")
       .schema(customer_schema)
       .load("/public/trendytech/datasets/customer_nested/*")
   )
   ```

## Date types

- Default format of date  type  in spark is yyyy-mm-dd 

- If the date is in differenty format will lead to parser error

- If all the collumns have identical date format the we can set the date format as
  
  ```python
  df = (
      spark.read
      .format("csv")
      .schema(order_schema)
      ,option("dateFormat", "MM-dd-yyyy")
      .load()
  )
  ```

- If we have different date format we can read the columns then transform to date format
  
  ```python
  from pyspark.sql.functions import to_date
  order_schema = 'order_id long, order_date string, cust_id long, order_status string'
  
  df = (
      spark.read
      .format("csv")
      .schema(order_schema)
      ,option("dateFormat", "MM-dd-yyyy")
      .load()
  )
  df = df.withColumn("order_date", to_date("order_date", "MM-dd-YYYY"))
  ```

```
> Note: In case of Parse Issues, the complete date column shows up as null.



## Dataframe Read Modes

1. **Permissive** (default):- In case of Data type missmatch convert the values to Null without impacting the rest of the results

2. **failfast** Throws an error on encountering the malformed records

3. **dropmalformed** Any malformed records will be eliminatedd and the rest of the records in proper shape will be processed. 



> Note: You can choose the respective read modes based on the business
> requirement.



## Creating a Dataframe

- Using spark.read

```python
df = spark.read.format("csv").option("header","true").load(filePath)
```

- Using spark.sql
  
  ```python
  df = spark.sql(“select * from <table-name>”)
  ```

- Using spark.table
  
  ```python
  df = spark.table(“<table-name>”)
  ```

- Using spark.range
  
  ```python
  df = spark.range(<range-size>)
  df = spark.range(<start-range>, <end-range>)
  df = spark.range(<start-range>, <end-range>, <increment>)
  ```

- Creating Dataframe from Local List
  
  ```python
  df = spark.createDataFrame( list )
  
  df = spark.createDataFrame( list ).toDF(<column-name>)
  
  df = spark.createDataFrame( list, schema )
  ```

- Creating Dataframe from RDD
  
  ```python
  df = spark.createDataFrame( RDD, schema )
  df = spark.createDataFrame( RDD ).toDF(<column-name>)
  df = rdd.toDF(<column-name>)
  ```

## Dataframe Transformations

1. withColumns :- Add new Column or change existing columns
   
   ```python
   df = df.select("column1", expr("expression"))
   df = selectExpr("list of column name and expression")
   ```

2. withColumnRenamed:- To rename the existing column
   
   ```python
   df = df.withColumnRenamed("old_name", "new_name")
   ```

3. drop :- to remve a column
   
   ```python
   df = df.drop("column_name")
   ```

> Note:
> -
> 
> - In case of “select” we will have to explicitly segregate the column
>   names and expressions and mention the expressions used within
>   an expr.
> 
> - In case of “selectExpr”, it automatically identifies whether the
>   value passed is a column name or an expression and accordingly
>   actions it.

## Removal of duplicates from Dataframe

1. df2 = df1.distinct() [removes duplicates when all the columns are
   considered]
2. df2 = df1.dropDuplicates() [removes duplicates when a subset of
   columns are considered]

## Creation of Spark Session

- Spark Session acts as an entry point to the Spark Cluster. To run the code on Spark Cluster, a Spark Session has to be created.

- In order to work with Higher Level APIs like Dataframes and Spark SQL, Spark Session has to be created to run the code across the cluster.

- To work at RDD level, Spark Context is required.

- Spark Session acts as an umbrella that encapsulates and unifies the different contexts like Spark Context, Hive Context, SQL Context...

![](media/005_spark_dataframe/8e5545cfd0e7ec631f40241c5295d04dda63d563.svg)






