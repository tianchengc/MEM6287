## 🗃️ Hadoop Architecture: HDFS & MapReduce

### Hadoop Distributed File System (HDFS)

> **HDFS** is a distributed file system designed for reliable, fault-tolerant storage of very large files by splitting them into smaller blocks and distributing these blocks across multiple nodes in a cluster.

| Concept | Description |
| --- | --- |
| **Block Size** | Files are split into blocks of 64MB (Hadoop 1.x) or 128MB (Hadoop 2.x). The last block may be smaller. |
| **NameNode** | Manages the file system namespace and metadata, including block locations and replication info. |
| **Secondary NameNode** | Runs on a separate host; acts as a buffer that periodically merges EditLogs with FSImage to checkpoint the filesystem state. It is NOT a backup for failover. |
| **DataNode** | Stores actual data blocks, handles read/write requests, and sends heartbeat signals to the NameNode every 3 seconds to report status. |
| **Replication** | Blocks are replicated (`default 3x`) across different nodes and racks to ensure fault tolerance and high availability. |
| **Fault Tolerance & Availability** | Data blocks are stored on different racks to ensure redundancy and availability if a node or rack fails. |
| **File Storage Example** | A 612 MB file with 64 MB block size breaks into 10 blocks (9 full 64 MB blocks + 1 block of 36 MB). |

### HDFS Components and Their Roles

| Component | Role |
| --- | --- |
| NameNode | Maintains metadata including FSImage (file system namespace) and EditLog (transaction log of file ops). |
| Secondary NameNode | Periodically merges EditLog with FSImage to create checkpoints, assisting in recovery but not failover. |
| DataNode | Holds actual data blocks, responds to client read/write requests, sends heartbeats to NameNode regularly. |

### Key Facts About HDFS

- Optimized for **streaming reads** of large files rather than random access.
- Works best with **fewer large files** (typically 100MB+), handling millions but not billions of files efficiently.
- Files are generally **write-once, read-many**.
- The NameNode is a **single point of failure** in Hadoop 1.x; secondary NameNode helps with checkpointing but does not provide failover.

---

## 🖥️ Hadoop MapReduce

> **MapReduce** is a programming model and framework designed to process large datasets in a distributed Hadoop cluster by dividing work into map and reduce tasks that execute close to the data (data locality).

### MapReduce Processing Model

| Phase | Description |
| --- | --- |
| **Map** | Processes input data by converting it into key/value pairs. Each Map Task operates on a data split. |
| **Reduce** | Aggregates or summarizes the output from Map tasks based on keys to produce the final result. |

### MapReduce Architecture Components

| Component | Role |
| --- | --- |
| Job Tracker | Master node that schedules, monitors, and coordinates jobs across the cluster. Determines execution plans. |
| Task Tracker | Runs on DataNodes, executes map and reduce tasks assigned by Job Tracker, and sends status updates (heartbeats). |

### Job Tracker vs Task Tracker

| Feature | Job Tracker | Task Tracker |
| --- | --- | --- |
| Role | Master daemon managing job scheduling & coordination | Executes map/reduce tasks on DataNodes |
| Location | `Runs on NameNode` | Runs on each DataNode |
| Failure Handling | Reschedules failed tasks to other Task Trackers | Sends heartbeat signals to Job Tracker |
| Job Monitoring | Tracks job progress and status | Reports task status and progress |

---

## 📊 Key Concepts in Hadoop Data Processing

| Concept | Explanation |
| --- | --- |
| **Data Locality** | Instead of moving large data volumes to the processing unit, Hadoop moves computation to the data location. This reduces network congestion and improves throughput. |
| **Block Replication** | Blocks are replicated across nodes and racks (`default replication factor = 3`) to ensure fault tolerance and high availability. |
| **Heartbeat Mechanism** | DataNodes send heartbeats every `3 seconds` to the NameNode; missing heartbeats for `10 minutes` mark a DataNode as out-of-service, triggering replication of its data. |
| **HDFS File Splitting** | Large files are split into blocks; the number of blocks is calculated by integer division plus one for any remainder block. |
| **Fault Tolerance & Scalability** | HDFS is designed for large-scale storage with no file size limits and built-in reliability through replication and distributed storage. |

---

## 🔄 Hadoop History and Ecosystem

- **Origins:** Hadoop evolved from the Apache Nutch project, inspired by Google's publications on the Google File System (GFS) and MapReduce.
- **Key Contributors:** Doug Cutting started Hadoop and later joined Cloudera, a company providing commercial Hadoop distributions.
- **Milestones:**

| Year | Event |
| --- | --- |
| 2003 | Google publishes GFS paper |
| 2004 | Google publishes MapReduce paper |
| 2005 | Hadoop sub-project created out of Nutch |
| 2008 | Hadoop becomes a top-level Apache project; Cloudera founded |
| 2010 | Hadoop 2.x released with YARN |
| 2012-13 | Hadoop ecosystem tools like Hive, Pig, and HBase graduate |

- **Ecosystem Components:**

| Tool/Component | Function |
| --- | --- |
| Pig | Data flow scripting language for Hadoop |
| Hive | SQL-like query language for Hadoop data |
| HBase | NoSQL database on top of HDFS |
| Zookeeper | Coordination service for distributed systems |
| Oozie | Workflow scheduler for Hadoop jobs |

---

## ⚙️ Hadoop 1.x Features & Limitations

| Feature | Description |
| --- | --- |
| Single NameNode | Acts as the master node managing metadata, a single point of failure. |
| Secondary NameNode | Performs checkpointing but cannot replace NameNode on failure. |
| MapReduce Job Tracker | Schedules and monitors jobs; runs on NameNode. |
| DataNodes | Store data and execute tasks. |
| Limitations | Scalability limited due to single NameNode and job tracker; failure recovery is manual and slow. |

---

## 🧮 Example: Calculating HDFS Data Blocks for a File

- Given a file size of 612 MB and default block size of 64 MB (Hadoop 1.x):

$$\text{Number of full blocks} = \left\lfloor \frac{612}{64} \right\rfloor = 9$$

$$\text{Size of last block} = 612 - (9 \times 64) = 36 \text{ MB}$$

- **Total blocks = 9 full blocks + 1 partial block = 10 blocks**

---

## 💡 Important Notes on Data Locality and Processing

- Hadoop’s design principle is to **process data where it is stored**, not to move data to the computation.
- Analytics applications should be **topology-aware**, meaning they know the data node locations to optimize task assignment.
- This design significantly **improves throughput** by minimizing network data transfer.

---

## 📚 Summary of Key Terms

| Term | Definition |
| --- | --- |
| **NameNode** | Metadata manager of HDFS, tracks file-to-block mappings and replication. |
| **Secondary NameNode** | Supports NameNode by checkpointing metadata; not a failover node. |
| **DataNode** | Stores blocks, executes read/write, sends heartbeat to NameNode. |
| **Map Task** | Processes input data into key/value pairs. |
| **Reduce Task** | Aggregates map outputs based on keys to produce final results. |
| **Job Tracker** | Master scheduler for MapReduce jobs. |
| **Task Tracker** | Executes MapReduce tasks on DataNodes and reports status. |
| **Data Locality** | Moving computation to data rather than moving data to computation. |

---

This concludes the detailed notes on **Batch Processing of Big Data** including Hadoop architecture, HDFS, MapReduce, and ecosystem components as covered in Week 5 of MESM 6287 Advanced Data Analytics.

## 🔄 MapReduce Framework and Word Count Example

### MapReduce Components

| Component | Functionality |
| --- | --- |
| **Map** | Processes input data splits (e.g., lines), emits intermediate key-value pairs (e.g., words and counts) |
| **Shuffle** | Redistributes and groups map outputs by key to prepare for reducing; performs local aggregation |
| **Reduce** | Aggregates data from shuffle phase, producing final output |

### Word Count Example Workflow

1. Input data is split into lines; each split is assigned to a **map task**.
2. Each map task emits words with count 1 from its assigned lines.
3. A **shuffle task** aggregates identical words from all map outputs.
4. The **reducer** counts the total occurrences of each word.
5. Final output is combined from reducer outputs.

### Important Execution Notes

- Map task outputs are written to **local node disks**, not HDFS, to avoid unnecessary replication.
- Once reduce tasks complete, map outputs can be discarded.
- If a node fails before its output is consumed, Hadoop reruns the map task on another node.
- Reduce tasks do **not** follow data locality since they require data transfer from map outputs.
- Reduce outputs are stored in **HDFS** for reliability.

---

## ⚠️ Hadoop 1.x Limitations

| Limitation | Explanation |
| --- | --- |
| Intermediate files on disk | Causes slower processing due to frequent disk I/O |
| Fixed Map & Reduce slots | MapReduce handles both resource management and processing, limiting flexibility |
| Synchronization barriers | All map tasks must finish before reducers start, causing delays |
| NameNode is SPOF (Single Point of Failure) | Failure of NameNode disrupts entire cluster operation |
| Single Job Tracker | Only one job can run at a time, creating bottlenecks |
| Job Tracker Overload | Can be overwhelmed managing large clusters |
| Max cluster size | Supports up to 4,000 nodes |

---

## 🚀 Hadoop 2.0 Enhancements

| Feature | Description |
| --- | --- |
| **Scalability** | Supports clusters with over 10,000 nodes |
| **Increased HDFS block size** | Default block size increased to 128 MB for better throughput |
| **High Availability (HA)** | Supports multiple NameNodes with Active-Passive failover configuration |
| **Cluster Utilization** | YARN enables running multiple applications, not just MapReduce |
| **Multi-tenancy** | Allows multiple jobs to run simultaneously |

### Hadoop 2.0 Ecosystem Components

| Component | Role |
| --- | --- |
| **HDFS2** | Reliable, redundant storage |
| **YARN** | Cluster resource management |
| **MapReduce** | Batch data processing |
| **Pig** | Data flow scripting platform |
| **Hive** | SQL-like querying |
| **Tez** | Execution engine for batch and streaming jobs |
| **HBase** | Distributed NoSQL database |
| **Others** | Cascading, Storm, Graph processing frameworks |

---

## 🧑‍💻 NameNode Improvements in Hadoop 2.x

- Supports **multiple NameNodes** for fault tolerance.
- Operates in **Active-Passive** configuration with automatic failover.
- Application data split into **namespaces** for better management.
- All metadata edits logged to a **shared NFS storage**.
- Passive NameNode reads from shared storage to maintain updated metadata.
- **Fencing mechanism** ensures only one NameNode writes to shared storage at a time.

---

## 🗂️ Yet Another Resource Negotiator (YARN)

### Purpose

> Designed to separate resource management from MapReduce processing and improve job scheduling.

### Key Components

| Component | Description |
| --- | --- |
| **Container** | Allocates physical resources (disk, CPU, RAM) on a node for a task; also called Container Launch Context (CLC) |
| **Application Master** | Manages lifecycle and health of a single submitted job; sends container requests to Node Managers |
| **Node Manager** | Manages containers on individual nodes and reports node health to Resource Manager |
| **Resource Manager** | Oversees cluster resource allocation, schedules jobs, and works with Node Managers |

### YARN Workflow

- Clients submit jobs to Resource Manager.
- Resource Manager allocates containers on nodes.
- Application Master manages job execution inside containers.
- Node Managers monitor resources and container health.

---

## 🐖 Apache Pig

### Overview

- Procedural data flow language for Hadoop.
- Simplifies writing MapReduce jobs by providing **Pig Latin** scripting.
- Translates Pig Latin scripts into MapReduce jobs executed on Hadoop.

### Pig Data Types

| Data Type | Description | Example |
| --- | --- | --- |
| **Atom** | Simple atomic value (string, number, etc.) | `'text'`, `'2.0'` |
| **Tuple** | Ordered set of fields of any type | `<text, 2.0>` |
| **Bag** | Unordered collection of tuples | `{(Course, 'ELG'), (Code, 5166)}` |
| **Map** | Collection of unique key-value pairs | `[('key1', 3), ('key2', 4)]` |

### Pig Workflow

1. Load data from local files or HDFS.
2. Process data using operations:

    - **Filter:** Apply expressions to select records.
    - **Join:** Combine records based on conditions.
    - **Group:** Aggregate records by keys.
    - **Foreach:** Apply expressions to each record.3. Pig Latin focuses on data flow, **no control flow constructs** like if statements or loops.

---

## 🐝 Apache Hive - Hadoop SQL

### Purpose

- Data warehouse infrastructure on Hadoop for processing **structured data**.
- Developed at Facebook, now Apache project.
- Enables Big Data summarization with **SQL-like queries** (HiveQL).
- Designed for **OLAP (Online Analytical Processing)**, not OLTP.
- Translates HiveQL queries into MapReduce jobs for execution.

### Hive Components & Workflow

| Component | Role |
| --- | --- |
| **Map Operator Tree** | Processes data splits during Map phase |
| **SerDe** | Serialization/Deserialization for data formats |
| **Execution Engine** | Coordinates job execution |
| **MetaStore** | Stores metadata about tables, partitions, schemas |
| **Driver** | Compiles HiveQL, manages lifecycle |

---

## 💻 HiveQL Examples

### Creating a Table
```sql
CREATE TABLE IF NOT EXISTS employee (
  eid int,
  name String,
  salary String,
  destination String
)
COMMENT 'Employee details'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
LINES TERMINATED BY '\n'
STORED AS TEXTFILE;
```
### Loading Data into Table
```sql
LOAD DATA LOCAL INPATH '/home/user/sample.txt' OVERWRITE INTO TABLE employee;
```
### Sample Employee Data

| eid | name | salary | destination |
| --- | --- | --- | --- |
| 1201 | Gopal | 45000 | Technical manager |
| 1202 | Manisha | 45000 | Proof reader |
| 1203 | Masthanvali | 40000 | Technical writer |
| 1204 | Kiran | 40000 | Hr Admin |
| 1205 | Kranthi | 30000 | Op Admin |

### Table Modification Commands

| Command | Description |
| --- | --- |
| `ALTER TABLE name RENAME TO new_name` | Rename a table |
| `ALTER TABLE name ADD COLUMNS (col_spec[, col_spec ...])` | Add columns to a table |
| `ALTER TABLE name DROP [COLUMN] column_name` | Drop a column |
| `ALTER TABLE name CHANGE column_name new_name new_type` | Change column name and type |
| `ALTER TABLE name REPLACE COLUMNS (col_spec[, col_spec ...])` | Replace all columns |

### Example: Extending Employee Table
```sql
ALTER TABLE employee ADD COLUMNS (dept STRING COMMENT 'Department name');
ALTER TABLE employee REPLACE COLUMNS (
  eid INT,
  empid INT,
  ename STRING,
  name STRING
);
```
---

## 🐘 Apache ZooKeeper

### What is ZooKeeper?

> Open-source distributed coordination service for distributed applications, developed at Yahoo Research.

### Key Functions

- Maintains configuration information.
- Provides a naming registry.
- Coordinates distributed processing.
- Synchronizes distributed applications.
- Acts as a central repository for configuration settings.
- Enables other libraries to leverage its coordination services.

---

## 🧩 ZooKeeper Architecture and Operation

| Aspect | Details |
| --- | --- |
| **Modes** | - **Standalone**: single server, no replication.   - **Quorum**: ensemble of ≥3 servers with replication. |
| **Server Role** | Maintains in-memory state, transaction logs, and snapshots on persistent storage. |
| **Clients** | Connect to a single server at a time; maintain state via requests/responses, watch events, heartbeats. |
| **Failover** | If server connection lost, client connects to another server. |
| **Read/Write Load** | Optimized for read-heavy workloads with read:write ratio ~10:1. |
| **Leader and Followers** | - **Leader**: elected at startup, responsible for recovery and coordination.   - **Followers**: obey leader instructions. |

---

# End of Notes

## 🗃️ Apache HBase

> **HBase** is the Hadoop database designed for **distributed, scalable big data storage**.

### Key Features of HBase

| Feature | Description |
| --- | --- |
| Based on | Google BigTable (NoSQL, column-oriented) |
| Storage | Built on top of HDFS (Hadoop Distributed File System) |
| Data Model | Column-family oriented, with column data stored together in a single HFile |
| Use Case | Random, real-time, read/write access to Big Data stored in HDFS |
| Performance | Supports **low-latency record seek** for accessing rows among millions of records |
| Difference from HDFS | HDFS supports high-latency batch processing, no random read/write; HBase adds low-latency access |

### Improvements Over HDFS

- HBase provides **low-latency random reads and writes** on top of HDFS.
- Can handle **petabytes of data**.
- Supports **Auto-Sharding**: automatic dynamic distribution of tables when too large.

### HBase Architecture

| Component | Role |
| --- | --- |
| HMaster (Master) | Handles table creation, modification, deletion; single point of failure (SPOF) |
| Region Servers | Handle actual data reads/writes for assigned row key regions (HTable operations) |
| Zookeeper | Manages cluster coordination and state |

- Clients interact with **HMaster only for metadata operations**.
- Data reads/writes go directly to the responsible **Region Server**.
- HFile stores sorted key/value pairs (both keys and values are byte arrays).
- HBase depends on **NameNode** and **HMaster** (both SPOFs).

---

## 🗂️ HBase Meta Table

> The **META table** keeps track of which Regions are assigned to which Region Servers.

### META Table Details

| Aspect | Description |
| --- | --- |
| Structure | A **B-tree** data structure |
| Key | Region start key and region ID |
| Value | The Region Server responsible for that region |
| Purpose | Used to find the Region Server managing a specific table key |

### Data Flow in HBase

- Data is **initially stored in MemStore** as sorted key/value pairs.
- When MemStore fills, the data is written to a new HFile in HDFS as a **sequential write**, which is very fast because it avoids random disk seeks.

---

## 🔄 Apache Oozie

> **Oozie** is a **workflow scheduler system** for managing Hadoop jobs.

### Features

- Allows creation of workflows incorporating jobs from various libraries including:

    - MapReduce
    - Pig
    - Hive
    - Sqoop
    - Java applications- Workflows can be triggered by:

    - Time (scheduling)
    - Data availability
---

## 🔄 Apache Sqoop

> **Sqoop** is a tool for **transferring data** between Hadoop and relational databases (RDBMS).

### Sqoop Workflow

| Direction | Description |
| --- | --- |
| RDBMS → HDFS | Importing data from relational DBs into Hadoop Distributed File System |
| HDFS → RDBMS | Exporting data back to relational databases |
| RDBMS ↔ HBase/Hive | Transfers between relational DBs and HBase or Hive |

---

## 📥 Apache Flume

> **Flume** is a service for collecting, aggregating, and moving large amounts of streaming log data into Hadoop.

### Flume Components

| Component | Role |
| --- | --- |
| Source | Retrieves streaming data and sends it to the Channel |
| Channel | Acts as a buffer or queue between Source and Sink |
| Sink | Delivers data to the destination, such as HDFS or HBase |

- Commonly used for ingesting large volumes of log data.
- Can listen to live log events or ingest log files.

---

## ⚡ Apache Storm - Event Stream Processing

> **Storm** provides **real-time data processing** for streaming data.

### Key Concepts

| Term | Definition |
| --- | --- |
| Tuples | Ordered list of elements, e.g., a 4-tuple (7, 1, 3, 7) |
| Streams | Unbounded sequences of tuples |
| Spouts | Sources of streams, e.g., Twitter API |
| Bolts | Process input streams; can run functions, filter, aggregate, join data, or interact with DBs |
| Topologies | Visual representation of computation as a network of spouts and bolts |

### Comparison: Flume vs. Storm

| Feature | Flume | Storm |
| --- | --- | --- |
| Purpose | Injects large volumes of log data | Purely streaming real-time data |
| Processing | Streaming or batch | Streaming only |
| Use Cases | Log data ingestion | Real-time analytics, ML, monitoring |

---

## ⚙️ Apache Spark

> Spark is a **parallel distributed processing framework** known for **in-memory computation**.

### Spark Features

| Feature | Description |
| --- | --- |
| General Purpose | Supports a variety of workloads |
| Distributed Storage Support | Works with HDFS, Cassandra, HBase, Amazon S3 |
| Supported Languages | Scala, Python, Java, R |

---

## 🤖 Apache Mahout

> Mahout is a **machine learning library** originally designed to run on Hadoop clusters using MapReduce.

### Mahout Evolution and Features

| Aspect | Description |
| --- | --- |
| Initial Purpose | Collection of common ML algorithms running on Hadoop MapReduce (YARN or MapReduce v1) |
| Transition | Shifted to Spark in 2014 for better performance |
| Current State | Backend-independent, supports non-Hadoop clusters and single-node execution |
| Programming Interface | Provides an R-like Domain Specific Language (DSL) |
| Algorithm Coverage | Both supervised and unsupervised ML algorithms |

### Algorithms and Functions in Mahout

| Category | Examples |
| --- | --- |
| Classification | Naïve Bayes, Random Forest |
| Clustering | K-Means, Fuzzy K-Means, Canopy, Streaming K-Means |
| Other Algorithms | Lanczos Algorithm, Dirichlet Clustering, Spectral Clustering, Hidden Markov Models, Frequent Pattern Matching, Matrix Factorization, Stochastic Gradient Descent |
| Mathematical Functions | Matrix functions, Vector functions |

---

## 🏆 Hadoop Success Stories

### Yahoo

| Metric | Details |
| --- | --- |
| Cluster Size | Over 100,000 CPUs across 40,000+ computers |
| Largest Cluster | 4,500 nodes (each node 2x4 CPU, 4x1TB disks, 16GB RAM) |
| Data Stored | Over 455 Petabytes |
| Daily Jobs | Over 850,000 Hadoop jobs |
| Usage | 60% of jobs use Apache Pig |
| Application | Ad systems, web search research |

### Facebook

| Metric | Details |
| --- | --- |
| Data Ingested Daily | 12 TB of compressed data |
| Data Scanned Daily | 800 TB of compressed data |
| Jobs per Day | 25,000 map-reduce jobs |
| Number of Files | 65 million files in HDFS |
| Simultaneous Clients | 30,000 clients connected to NameNode |
| Usage | Searching, log processing, recommendation systems, data warehousing, video/image analysis |
| Popular Apps | Lexicon (user experience), Messenger (based on HBase) |

---

## ⚠️ Hadoop Limitations

| Limitation | Explanation |
| --- | --- |
| Small Files Problem | HDFS is inefficient with many small files; must merge into larger files |
| Slow Processing Speed | MapReduce processes large distributed data slowly; unsuitable for quick answers |
| Latency | Processing latency can range from minutes to days |
| Security | No strong segmentation or encryption of data at rest in Hadoop clusters |
| No Real-Time Processing | Hadoop supports batch processing only, no real-time data processing |
| Verbose Coding | MapReduce programming is Java-based and can result in lengthy code |
| Complexity | Managing Hadoop applications is complex; tools like Zookeeper help manage complexity |