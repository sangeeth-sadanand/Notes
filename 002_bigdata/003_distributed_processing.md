# Distributed processing

## MapReduce

- MapReduce is a Programming Paradigm
- MapReduce has 2 phases: 
  1. Map
  2. Reduce

![](media/003_distributed_processing/a8aa7e8ed155ef47d4a6edf4d7718b474f88c422.svg)

- Both takes (key, value) pair as input and output.

- Map phase gives **parallelism**

- Reduce is used to **aggregate** data.

- A good MapReduce code is by adding more code process on the mappers & keep least processing into reduces part.

- Parallelism is constraint based on the hardware

- No. of mappers is equal to No. of blocks for a data.

- No. of reducers can be controlled by developers, by default is 1.

- We can increase the number of reducers, It may improve the performance.

- In a use case such as filtering the data we may not use reducer at all.

- Shuffle and sort is used only when 1 or more reducer are used.

- Concept of partition comes to play when we have more than one reducer.

- ![](media/003_distributed_processing/101b2b57abbcf78c8039f0c1c93c94bad97612f6.svg)

- By default we have a hash function to determine which partition to a specific partition

- The partition calculated using hash of the key is consistent ensuring same key is assigned to a reducer.

- We can use Combiners to increase the parallelism at the mapper end

### How the MapReduce works with multiple reducer?

![](media/003_distributed_processing/958244eb066cd2f33255b533dae4dd53f9263910.svg)

### Challenges with Map reduce

1. Performance - lot of Disk IO's
2. Its really hard to write the code 
3. Map reduce only support batch processing & does not support streaming. 
4. learning Curve is high 
5. In Map reduce every thing is to in form of Map reduce 
6. Do not have interactive mode

## Spark

- Spark is general purpose, In memory Compute engine
- Distributed processing | compute engine
- Spark does not come with storage or resource engine
- Storage can be HDFS / S3 / ADLS Gen2 / GCS / local
- Resource manager can be YARN / Mesos / Kubernetes
- Spark is a multi language engine for executing data engineering, data science and machine learning on single node or cluster
- Spark abstracts away distributed machine
- In case of map reduce to write and read happens after Map reduce job
- In case of sparks IO write are reduce.

![](media/003_distributed_processing/6ad823d896f527f96b3fdfefad21b6b68760e9e8.svg)

- Spark has two layers
  - Layer 1 - Spark Core API (Works with RDD) can write code in Scala, Python, Java and R
  - Layer 2 - Higher level API (Dataframe, Spark SQL, Structured streaming, MLlib, Graphx)
- With spark we can work on 3 ways
  * [RDD](./rdd.md)
  * [Data frame](005_spark_dataframe.md)
  * SQL

### RDD

- When we work with Spark core we work with RDD
- RDP - resilient distributed dataset
- Resilient in RDD is due to immutability of data
- We can work with RDD which is hardest

### Operations

- Spark has 2 kind of operations
  
  1. Transformation
  2. Actions

- During transformation phase it creates an execution plan of the job

- Sparks only execute the plan

- when any action operation is triggered

- Spark performs lazy operation as it can optimize the operation steps.

### Spark Vs Data brick

- Spark is open source
- Databrick is a product which has spark with extra feature like
  - spark on cloud AWS |Azure | GCP
  - optimize spark
  - It contains Cluster manager
  - Delta lake
  - Collaborate Notebook
  - Implements security
