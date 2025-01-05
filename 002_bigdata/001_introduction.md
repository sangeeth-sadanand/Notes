# Big data - An introduction

## What is big data?

- In layman's language "data that cannot be processed or stored on a single computing system".
- More formal definition given by IBM is governed by 3V's / 5V's.
  - **Volume**: Data that is huge cannot be stored in one machine.
  - **Variety**: Data with variety of format, can be structured, unstructured or semi-structured.
  - **Velocity**: Speed at which data is inserted and consumed.
  - **Veracity**: The quality or correctness of the data.
  - **Value**: Should able to generate value out of the data

## Monolithic Vs Distributed system

- **Monolithic** :- One big system that holds a lot of resources and thereby high computation power. Performance does not increase in same ratio as the resource.
- Distributed system:- Is a cluster of system grouped together with each other holding its own resources. To scale up you need to increase node.

## Hadoop overview

### What is Hadoop?

- It is framework to solve big data problems. 
- It is combination of tools and technologies to solve big data problem.
- There are 3 core components
  1. **HDFS (Hadoop Distributed File System)**: It take care of storage
  2. **MapReduce**: Distributed processing 
  3. **YARN(Yet Another Resource Negotiator)**: Resource manager
- Writing a map reduce is really hard.-Java it is obsolete.
- Hadoop has three major version
  - Hadoop 1 - 2007 
  - Hadoop 2 - 2012
  - Hadoop 3 - Current version

### Hadoop eco-system

- **Sqoop**:- Migrate data from dB to HDFS and vise a versa.
- **Pig**:- It is a scripting language It helps in clean and process the data it is outdated language.
- **Hive**:- Provides a SQL interface to query a data.
- **Oozie**:- A workflow scheduler.
- **HBase**:- is a NoSQL database.

![](media/001_introduction/6cad139b5960356b92ed3643594d330631d0f4c9.svg)

### Challenges with Hadoop

- Map reduce is very slow and its really hard to write the MapReduce code.
- We need to write learn so many different components and each has its own big learning curve.
- It is mostly used for on-premises system.

### Internals of HDFS

- HDFS follows a master (name node), slave (data node) architecture

![](media/001_introduction/1fd54c9e580a33ebfaf747a711e2fc64ccbf8721.svg)

#### Name node:

- It holds the meta data. i. e. it stores the where the sub files are stored in each data node

#### Data node:

- Node where actual data is stored
- Current version of HDFS has 128 MB as block size
- Whenever a client wants a file it goes to name node
- Redundancy of data is kept in multiple nodes which is governed by replication factor Currently replication factor is 3 by default mean the data is replicated in 3 nodes is kept.
- Every Data node sends a live signal or heartbeat to name node every specific interval.
- When ever the a name node fails secondary name node takes its place.

## Cloud and it's advantages

- 3 types of cloud services
  - **Public cloud** - [AWS, Azure, GCP] 
  - **Private cloud** - with in the organization 
  - **Hybrid cloud** - Public + Private

### Advantages

- Scalable
- No requirement of Capital Expense only require Operational Expense
- Agile
- Geo-distribution
- Disaster recovery
- Cost effective.

## What is Apache Spark?

- Mapreduce is biggest bottle neck.
- Apache spark is general purpose, in-memory, compute engine
- Sparks replaces Mapreduce
- Spark needs storage and a resource manage.
  - **Storage** - HDFS, S3, ADLS Gen2, GCS, local storage 
  - **Resoure manager** - YARN, Mesos, Kubernetes
- Its a plug & play compute engine.
- Spark code can be written in scala, python, java and R.
- Spark itself is written in scala.

## Database Vs Data warehouse Vs Datalake

### Database

- Transactional data
- Online transactional processing.
- Structural data
- Recent data
- Schema on write
- **Example**: Oracle, MySQL

### Data warehouse

- Analytical processing where historical data is required to find insight.
- In database, complex queries can reduce the speed of transactional process.
- We can migrate the data from database to data warehouse to do analytics.
- Structured data - Schema on write.
- Storage cost is high but less than database.
- it follows Extract, Transform & Load process.
- **Example**: Teradata

### Datalake

- To get insights from huge amount of data
- The data is present in raw format.
- It can be structure or unstructured format.
- It follows ELT process
- Cost effective
- Schema on read.

## Data engineering flow

![](media/001_introduction/1c671a66dfac6c58474278a88629b78d3c9e1202.svg)

### On-premises

![](media/001_introduction/6d97daec49cd81d2c500294acd03996be1004f8d.svg)

### Azure Cloud

![](media/001_introduction/e3387cf68909af06e530cd820eb3550d3b42affd.svg)

### AWS Cloud

![](media/001_introduction/462d3cd3e1d273783a6a2529cdb8e067932ed5d2.svg)

## Serverless v/s server based services

### Serverless

- **Example**: AWS Athena
- Will charge you  based on of data scanned.
- You will use resources from a shared pool will be less expensive.
- Since resources are not dedicated there-will be impact on performance

### Server based

- **Example**: Aws Redshift
- Need to turn on a dedicated cluster it will charge from the time it is turned on till it was switched off.

## Concept of Data

- Process the data where it is present Hadoop works on the principle of data locality.
