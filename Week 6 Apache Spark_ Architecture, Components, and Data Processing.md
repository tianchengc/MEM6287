# 📊 In-memory Data Processing using Apache Spark

## Apache Spark vs. MapReduce: The Challenge

MapReduce faces significant limitations when processing complex analytics:

- While cluster computing offers tremendous potential through **data locality**, MapReduce struggles with certain workloads
- **Iterative algorithms** (common in machine learning) require multiple passes (10-20) over data
- Each pass in MapReduce must be written as **separate MapReduce jobs** that:

    - Need to be launched separately
    - Load data from scratch each time
    - Write intermediate results to disk between stages
## What is Apache Spark?

> "Apache Spark is a fast general-purpose engine for large-scale data processing." - Apache.org

> "Spark is an `open-source` framework for in-memory big data processing built around the concept of speed, ease of use, ability to run everywhere, and sophisticated analytics." - spark.apache.org

Key characteristics:

- **Open-source** framework for in-memory big data processing
- Provides **access to data from various sources** including HDFS, OpenStack Swift, Amazon S3, and Cassandra
- Focuses on **speed**, **ease of use**, **versatility**, and **sophisticated analytics**

## Apache Spark vs. MapReduce: Advantages

| Feature | Apache Spark | MapReduce |
| --- | --- | --- |
| Speed | 100x faster, especially for multi-stage jobs | Slower due to disk I/O between stages |
| Programming | Easier APIs with multiple language bindings | More complex programming model |
| Language Support | Python, R, Java, Scala | Primarily Java |
| Processing Model | In-memory processing | Disk-based processing |
| Code Complexity | Simpler (see example below) | More verbose |

Example of Spark code simplicity:
```scala
val textFile = sparkSession.sparkContext.textFile("hdfs:///tmp/words")
val counts = textFile.flatMap(line => line.split(" "))
                    .map(word => (word, 1))
                    .reduceByKey(_+_)
counts.saveAsTextFile("hdfs:///tmp/words_agg")
```
## Spark Adoption and Usage

**Companies using Spark:**

- Tech giants: Yahoo, Amazon, eBay, Shopify, Alibaba, Uber, Spotify
- Scientific organizations: NASA, CERN, MIT, Harvard

**Commercial distributions:**

- DataBricks, IBM, Cloudera, Blue Data

**Scale and community:**

- Largest known Spark cluster: 8,000 nodes
- Active GitHub project with over 2,000 contributors and 45,000+ commits (as of Oct 2023)

**Why organizations use Spark:**

- 91% - Performance gains
- 77% - Ease of use
- 71% - Ease of deployment
- 64% - Advanced analytics capabilities
- 52% - Real-time streaming capabilities

## Performance Record

- In 2014, Spark held the world record in the "Daytona Gray" category for sorting 100TB of data:

    - Sorted 100TB on 207 EC2 machines in 23 minutes
    - Compared to Hadoop MapReduce: 72 minutes on 2,100 machines
    - **3x faster using 10x fewer resources**- Record later surpassed by Tencent Sort (a specialized sorting application, while Spark remains general-purpose)

## Spark History Timeline

| Year | Milestone |
| --- | --- |
| 2009 | - UC Berkeley AMP Lab published research paper "Spark Cluster Computing Working Sets"    - AMP Lab implemented Spark Core    - Scala interpreter integrated with Spark for scaling to 100s of nodes |
| 2011 | - AMP Lab added Shark engine (now Spark SQL)    - Various Spark projects initiated: Spark Streaming, MLlib, GraphX |
| 2013 | - Project grew to 100+ contributors across 30+ organizations    - Contributed to Apache Software Foundation    - DataBricks company launched by AMP Lab team |
| 2014 | - Spark 1.0 released    - Became top-level Apache project |
| 2016 | - Spark 2.0 released    - Introduced Structured Streaming |
| 2018 | - Project Hydrogen announced for distributed ML frameworks support |
| 2019 | - Spark 3.0 released with dynamic partition pruning, ANSI SQL compliance, new UI for structured streaming    - Latest release noted: Spark 4.0.1 (Sept 2025) |

## The Spark Ecosystem

**Technical foundation:**

- Written in Scala, runs in a JVM
- APIs based on functional programming principles
- Efficient in-memory data sharing across computation steps

**Deployment options:**

- `Standalone (client)`
- Cluster using YARN, Mesos, Kubernetes, etc.

**Language APIs:**

- Maintain consistent concepts across languages
- Translate `Java, Python, Scala, or R` into JVM instructions for driver processes

## Spark Philosophy

### 1. Unified Platform

- Supports diverse analytics (data loading, SQL queries, ML, streaming)
- Uses same computing engine and APIs across use cases
- Achieves high performance by optimizing across libraries
- Can combine various tasks into a single scan over distributed datasets

### 2. Compute Engine

- Handles data loading from storage systems and computation
- Unlike Hadoop, has **no permanent storage**
- `Supports diverse storage systems`:

    - Hadoop HDFS
    - Azure Storage
    - Amazon S3
    - NoSQL stores (Cassandra)
    - Kafka and message brokers- Focus on computation over data for compatibility with public storage and streaming

## Spark Core Components

### 1. Spark Core

- Handles basic I/O functionalities
- Schedules and monitors jobs on Spark cluster
- Manages task dispatching and networking with storage systems
- Provides fault recovery and memory management
- Spark Core convert DataFrames and DataSets to optimized RDDs before processing

### 2. Spark SQL

- Leverages declarative queries and optimized storage
- Supports SQL-like queries on Spark data
- Outputs distributed datasets

### 3. Spark Streaming

- Provides both batch processing and data streaming
- Enables unified applications handling both paradigms

### 4. MLlib

- Facilitates scalable machine learning pipelines
- Simplifies deployment and development

### 5. GraphX

- Provides access to graph and non-graph sources
- Enables flexible graph construction and transformation

## Spark Architecture

### Core Architecture

- **Spark Applications** are submitted to the **cluster manager**
- Cluster manager grants resources to applications
- A Spark Application consists of:

    - **Driver process** - The heart of the application
    - **Executor processes** - Perform the actual work
### Driver Process

- Maintains state details for the application's lifetime
- Analyzes, distributes, and schedules work across executors

### Executors

- Execute assigned code
- Report computation state back to the driver node

### Master/Worker Relations

- Multiple Spark applications can run simultaneously on a cluster
- Drivers and executors are simply processes that can run on same or different machines
- Executors run Spark code driven by any Spark language API

## SparkContext

- Before Spark 2.0, SparkContext was the entry point of any Spark application

# 🔥 Apache Spark Architecture and Components

## Spark Contexts and Sessions

Spark provides several context objects for different types of interactions:

- **SQLContext**: Used for SQL interactions
- **HiveContext**: Used for Hive interactions
- **SparkContext**: Required for lower-level APIs like RDDs

From **Spark 2.0** onwards, **SparkSession** encapsulates these different contexts and creates a new SparkContext for all operations.

## SparkSession

> SparkSession is currently the `entry point` to your Spark application.

Key characteristics of SparkSession:

- Controls the driver process
- A Spark application needs only a **single SparkSession**
- Used to execute user-def,ined computation across the cluster
- In Scala or Python, it is represented by a variable `spark`

Example use case:

- Creating a Spark DataFrame with column "name" containing 1,000 records with values from 0 to 999
- This range of numbers represents a distributed collection
- When run on a cluster, each part of this range exists on different executors

## Cluster Management

Spark supports three popular cluster managers:

| Cluster Manager | Characteristics |
| --- | --- |
| **Standalone Cluster** | Allows each application to run an executor on every node within the cluster |
| **YARN** | `Executors run only on worker nodes;` comes with most Hadoop distributions; only cluster manager that supports Spark security |
| **Apache Mesos** | `Executors run only on worker nodes`; provides rich resource scheduling capabilities; has fine-grained sharing options allowing Spark shell to scale CPU allocation across multiple commands |

## Running Spark on YARN

- Each Spark executor runs as a YARN container
- Unlike Map-Reduce which uses a container for each task, Spark hosts **multiple tasks within a single container**
- Supports two operating modes:

    - **yarn-client**: Used with development (interactive and debugging use cases)

          - In **Apache Spark on YARN**, the **Client** in the diagram you’ve shared refers to **the process that submits the Spark application** — this can be:

                  - a terminal user running spark-submit,
                  - a scheduled pipeline runner (e.g., Airflow, cron),
                  - a notebook (e.g., Zeppelin, Jupyter),
                  - or even a backend application.  - **yarn-cluster**: Used with production jobs
### YARN Client Mode

- Spark driver runs in the process that initiates a Spark Application
- Application Master requests executor containers from the YARN Resource Manager
- The client communicates with containers to schedule work after they start
- Suitable for applications requiring user input (spark-shell, PySpark) as the Spark driver runs inside the client process

### YARN Cluster Mode

- Spark driver runs in the Application Master
- Responsible for driving the application and requesting resources from YARN
- Runs inside a YARN container
- Client that triggers the Spark application can exit after initialization
- **Not suited for interactive use** of Spark

## Spark API Toolset

Spark provides a hierarchy of APIs:

### Low-level APIs

- Provide visibility to the cluster partitions
- Include **RDDs (Resilient Distributed Datasets)** and **Distributed Variables**

### Structured/High-level APIs

- Provide structure and management to Spark applications
- Include **DataFrames**, **Datasets**, and **SQL**
- Extended by **Structured Streaming**, **Advanced Analytics**, and various **Libraries & Ecosystem** components

## Resilient Distributed `Datasets` (RDDs)

> RDDs are the foundation of Spark, with virtually everything built on top of them.
> - DataFrames - no-type-safe, Scala, python, Java and R
> - DataSets - strong type, structured data, java and scala only

RDD characteristics:

- **Resilient**: Fault-tolerant and capable of rebuilding data on failure
- **Distributed**: Data is distributed among multiple nodes in a cluster
- **Dataset**: Collection of partitioned data with values

Important facts about RDDs:

- Structured APIs (DataFrames/DataSets) compile down to lower-level RDDs
- RDDs expose physical execution characteristics like partitions to users
- Best suited for operations like parallelizing raw data stored in memory on the driver machine
- `Python does not support RDDs directly` - only DataFrames, so RDDs in Python must be converted to DataFrames

Additional RDD facts:

- RDDs represent both data and transformations on data
- Can be created from Hadoop Input Sources, `parallelize()` datasets, or by transforming other RDDs
- Actions force calculations and return values
- **Lazy evaluation**: Nothing is computed until an action requires it
- Best for applications applying the same operation to all elements of a dataset
- Less suitable for applications making asynchronous fine-grained updates to shared state

## Word Count Example with RDDs

The lecture mentioned a word count example similar to the popular map-reduce example, demonstrating RDD usage.

## DataFrames

- Both a data structure and an `API`
- Similar to a table or spreadsheet
- Not unique to Spark (R & Python use similar concepts, but on a single machine)
- DataFrame API is used with high-level Spark components:

    - Spark SQL
    - Spark Streaming
    - MLlib
    - GraphX
### Data Partitioning in DataFrames

- Unlike traditional tables/spreadsheets, DataFrames can span 100-1000s of nodes
- Data Partitioning allows executors to perform work in parallel
- `A DataFrame partition sits on one node`
- Partitions determine the level of parallelism with multiple executors

## Datasets - Type-Safe Structured API

- `Available only in Scala & Java (not in Python & R due to dynamic typing) same as RDD`
- Provide ability to assign a Java/Scala class to records within a DataFrame
- Allow manipulation of classes as typed objects like Java ArrayList or Scala Seq
- Share the same transformations as DataFrames
- Allow more complex and strongly typed transformations

## RDD vs. DataFrame vs. Dataset

| Feature | RDD | DataFrame | Dataset |
| --- | --- | --- | --- |
| Schema | No schema (fits unstructured data) | Has schema (for structured data) | Has schema (for structured data) |
| Language Support | All languages | All languages | Only Java & Scala |
| Type Safety | Yes | No | Yes |
| Underlying Processing | Direct | Converted to optimized RDDs | Converted to optimized RDDs |

- Python users work with DataFrames due to Python being untyped
- In Java, DataFrame is no longer supported from Spark 2.x
- Schema provides an expressive way to navigate inside the data
- **RDD** is like a list of objects: [String, String, String], you can manipulate them but Spark doesn’t know their internal structure.
- RDD is type safe ( it is DataSet ) but no schema ( Spark doesn't know schema of RDD )

## Spark SQL

- Most used interface for Spark developers
- Processes structured data using DataFrames/Datasets
- Provides SQL2003-compliant interface for querying data
- Brings Spark power to both analysts and developers
- Standard interface for reading/writing to various data stores:

    - JSON, HDFS, Apache Hive, JDBC, Cassandra, MongoDB, Apache HBase, etc.- **Recommended approach** for development in Apache Spark 2.x or later
- RDD interface is available but recommended only if needs cannot be addressed within Spark SQL

## Data Processing Steps

1. **Ingestion**: Loading data from data sources
2. **Applying Data Quality Rules**: Applying Schema to data (Schema-on-read)
3. **Transformation**: Computation passes
4. **Publication**: Moving data to the console or an external source

# 🚀 Apache Spark: Jobs, Transformations, and Actions

## Spark Job Architecture

A Spark job consists of multiple components that work together in the distributed computation environment:

- **Job**: A parallel computation consisting of multiple tasks that get spawned in response to a Spark action (for example, save() or collect()).
- **Job Stages**: Each job gets divided into smaller sets of tasks, called stages, that depend on each other.

    - Spark tries to pack as many transformations as possible into the same stage.
    - Spark engine starts a new stage after a shuffle operation.- **Shuffle Operation**:

    - Apache Spark executes shuffles by first having the "source" tasks write shuffle files to local disk during their execution stage.
    - Subsequently, the downstream stage — responsible for grouping and data reduction — launches tasks that fetch their corresponding records from these shuffle files before performing computation.
## Sample Application Workflow

Here's a walkthrough of a sample Spark application:
```scala
import org.apache.spark.sql.functions.{concat, lit}
val df = spark.read.format("csv")
.option("header", "true")
.option("inferSchema", "true")
.load("data/authors.csv")
df = df.select(concat(<span data-type="inline-math" data-latex=""lname", lit(", "),"></span>"fname"))
val newPath = "jdbc:postgresql://localhost/spark_labs"
df.write.mode("overwrite").jdbc(newPath, "authors_fullname", props)
```
### Application Flow Timeline:

| Time | Action |
| --- | --- |
| t0 | Start of the application (main() is called) |
| t1 | Application (Spark Driver) connects to the master and gets a Spark session |
| t2/3/4 | Spark triggers distributed data ingestion to load data into RDDs using 3 Workers (executors); Partitions are created for the ingestion |
| t5 | Spark adds a transformation step to the flow for each executor |
| t6 | Processed result is then saved to an output database |

## Lazy Evaluation & Actions

> "Spark waits until the last moment to execute the graph of computation instructions."

Key aspects of lazy evaluation:

- Requires Spark to first build a plan of transformations
- Compile the plan
- Optimize the data flow from end-to-end using techniques such as predicate pushdown on DataFrames

**Actions** are needed to trigger transformations. Types of actions include:

- View data in the console
- Collect data from native objects in another language
- Write output to data sources

**Examples of actions**:

- count()
- reduce(func)
- collect()
- take(n)
- top()
- first()
- sum()
- aggregate()

## Transformations

Transformations in Spark are divided into two main categories:

### 1. Narrow Transformations

- Input partition contributes to only one output partition
- Spark will perform operations in a pipeline (Pipelining), and this is done in memory
- Each partition of the parent RDD is used by at most one partition of the child RDD
- Allow for pipelined execution on one cluster node
- Failure recovery is more efficient as only lost parent partitions need to be recomputed

**Examples**:

- map
- filter
- union

### 2. Wide Transformations

- Input partition contributes to many output partitions
- Forces Spark to write results to disk
- Multiple child partitions may depend on one parent partition
- Requires data from all parent partitions to be available and to be shuffled across the nodes
- If some partition is lost from all the ancestors, a complete re-computation is needed

**Examples**:

- groupByKey
- join with inputs not co-partitioned

## RDD Transformations

### Basic Transformations

- **map(func)**

    - Returns a new distributed dataset formed by passing each element of the source through a lambda function func.- **filter(func)**

    - Applies lambda functions to all elements of a distributed data set
    - Returns a new distributed data set with elements that ensure the function evaluates to true- **distinct()**

    - Applies to all elements of a distributed data set and returns a new set with unique elements- **union()**

    - Returns a new distributed dataset containing all elements from two distributed datasets- **intersection()**

    - Returns a new distributed dataset that contains an intersection of the elements in both input data sets- **subtract()**

    - Returns a new distributed data set with elements in the first but not in the second data set- **sample()**

    - Returns a new distributed data set containing n-ratio sampled elements subset of the existing data set
### Pair Transformations

Applied to each key/element in parallel, where normal transformations like map() are then applied to all elements of the collection:

- **groupByKey()** – converts key-value pair into key-result iterable pair
- **reduceByKey()** – produces a new data set with the total sum for each key
- **sortByKey()** – sorts a pair of distributed data sets
- **subtractByKey()** – returns a new data set with no key-value pair in self
- **countByKey()** – count the number of elements for each key of a DDS, and return the result as a dictionary using items()
- **join()** – return a DDS which contains all pairs of elements with matching keys in self and other DDS, like an inner-join function

## Spark Actions

Actions trigger the execution of transformations:

- **reduce(func)**: Aggregate the elements of the dataset using a function func (which takes two arguments and returns one). The function should be commutative and associative so that it can be computed correctly in parallel.
- **collect()**: Return all the elements of the dataset as an array in the driver program. This is usually useful after a filter or other operation that returns a sufficiently small subset of the data.
- **count()**: Return the number of elements in the dataset.

## Spark Immutability - Data APIs

- Spark Data APIs are immutable - Data cannot be changed after it's created
- Change is only possible through transformations
- Making Distributed Datasets immutable reduces the complexity of data synchronization

## Apache Spark Success Stories

- **OpenTable**: Uses Spark for training recommendation algorithms and for NLP of restaurant reviews to generate new topic models
- **Financial institutions**: Detect fraudulent transactions in real-time based on previous fraud footprints
- **Shopify**: Processed 67 million records in minutes to create a list of stores for partnership
- **eBay**: Leverages Spark clusters in the range of 2000 nodes, 20,000 cores and 100TB of RAM through YARN
- **MyFitnessPal**: Scans through food calorie data of about 80 million users