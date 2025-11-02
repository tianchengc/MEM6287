## 📚 Distributed Database Systems

> **Distributed Database Systems** store data on multiple nodes/sites connected by a communication network. Each node operates as an independent database system, but users access data transparently as if it were local.

---

### Key Characteristics of Distributed Database Systems

| Characteristic             | Description                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------|
| **Local Autonomy**          | Each node manages its own security, record locking, logging, data integrity, and recovery. Local operations only affect local resources. |
| **Non-reliance on Central Site** | Avoids Single Point of Failure (SPOF) by not depending on any single node.               |
| **Continuous Operation**    | Maintenance tasks (backup, recovery) must not degrade overall system performance noticeably. |
| **Location Agnostic**       | Analytical processes do not depend on or know the physical data location.                   |
| **Fragmentation Independence** | Applications remain unaware of how data is fragmented across nodes.                      |
| **Replication Independence**| Applications are unaffected by replica maintenance or synchronization.                      |
| **Distributed Query Processing** | Queries are decomposed into distributed transactions, supporting concurrency, deadlocks, and recovery. |
| **Hardware/Environment Independence** | Can operate across diverse hardware, OS, and network environments.                 |

---

## 💾 Distributed Data Storage Approaches

| Approach      | Description                                                                                 | Notes                                      |
|---------------|---------------------------------------------------------------------------------------------|--------------------------------------------|
| **Replication** | Multiple copies of data fragments are stored across different nodes for fault tolerance and faster access. | Improves availability but increases update costs. |
| **Fragmentation (Partitioning)** | Data is split into fragments stored at different nodes.                              | Fragments can be horizontal or vertical.  |
| **Hybrid**    | Combines fragmentation with replication by replicating each fragment.                        | Balances fault tolerance and performance. |

---

## 🔄 Database Replication

- **Definition:** Replication means storing copies of data fragments redundantly at two or more sites.
- **Fully redundant databases:** Every site contains a full copy of the database.

### Advantages of Replication

| Advantage         | Explanation                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------|
| **Availability**   | Failure of one site does not make data unavailable if replicas exist.                           |
| **Parallelism**    | Multiple nodes can process queries on the same data fragment simultaneously.                   |
| **Reduced Data Transfer** | Data is locally available at each site holding a replica, reducing network load.          |

### Disadvantages of Replication

| Disadvantage                | Explanation                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------|
| **Increased Update Cost**   | Each replica must be updated, increasing overhead.                                          |
| **Concurrency Control Complexity** | Concurrent updates to replicas risk inconsistency without specialized control mechanisms. |
| **Solution**                | Use a primary copy for concurrency control, propagate updates to secondary replicas.        |

---

## 📊 Fragmentation Approaches

### Horizontal Fragmentation

- **Definition:** Database records are divided into subsets (rows), distributed across multiple nodes.
- **Example:**

| Site 1                | Site 2           | Site 3          |
|-----------------------|------------------|-----------------|
| id: 1, Sebastian, M, 3 | id: 3, Garry, M, 8 | id: 4, Louis, F, 7 |
| id: 2, John, M, 5      |                  |                 |

### Vertical Fragmentation

- **Definition:** Each fragment contains a subset of attributes (columns) of the entity.
- **Example:**

| Site 1            | Site 2          |
|-------------------|-----------------|
| id, Name          | id, Sex, Age    |
| 1, Sebastian      | 1, M, 3         |
| 2, John           | 2, M, 5         |
| 3, Garry          | 3, M, 8         |
| 4, Louis          | 4, F, 7         |

---

## 🔪 Sharding

> Sharding is a fragmentation technique widely used in distributed databases for horizontal scaling.

| Feature                   | Description                                                                                   |
|---------------------------|-----------------------------------------------------------------------------------------------|
| **Scope**                 | Can be done within a single node or across multiple nodes.                                   |
| **Type**                  | Achieved via horizontal or vertical fragmentation.                                          |
| **Result**                | Horizontal scaling that supports big data and improves query performance.                    |

---

### Sharding Methods

| Method                 | Description                                                                                 | Challenges                                                                                     |
|------------------------|---------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| **Hash-Based Sharding** | Uses a hash function on record keys to assign shards, ensuring even data distribution.     | Node changes disrupt shard numbering; permanent shard numbers can fix this. Losing a shard risks data loss. |
| **Range-Based Sharding** | Splits data by key ranges, each shard holding a data subset with the same schema.          | Uneven data distribution and potential hotspots may occur.                                    |
| **Directory-Based Sharding** | Uses a lookup table to map keys to shards; client queries directory to locate shards.     | Directory lookup may reduce performance and can be a Single Point of Failure (SPOF).           |
| **Geo-Based Sharding**   | Data is partitioned by geographical location of users, improving performance by proximity. | Hotspots may arise if a location lacks enough nodes to handle load.                            |

---

## 🛡️ Shard Replica Sets

- **Purpose:** Provide redundancy within each shard through replica sets.
- **Features:**
  - Load balancer distributes workload among replicas.
  - Nodes may share the same or have multiple storage volumes.
  - Ensures fault tolerance and availability inside shards.

---

## ⚖️ Sharding Benefits and Drawbacks

| Benefits                                 | Drawbacks                                            |
|------------------------------------------|-----------------------------------------------------|
| Enables horizontal scaling for big data. | Database management becomes more complex.           |
| Improves query response times significantly. | Potential data loss or corruption risk depending on implementation. |
| Simplifies maintenance.                   | Performance issues may arise under some conditions. |
| Eliminates Single Point of Failure (SPOF). |                                                     |
| Uses cost-effective commodity servers or cloud VMs. |                                                     |

---

# Important Terminology

| Term                   | Definition                                                                                     |
|------------------------|------------------------------------------------------------------------------------------------|
| **Fragmentation**       | Dividing a database into smaller pieces (horizontal or vertical) stored across different nodes. |
| **Replication**         | Creating multiple copies of data fragments across nodes for fault tolerance and availability.  |
| **Shard**               | A fragment or partition of a database that forms part of the overall distributed system.        |
| **Shard Replica Set**   | A group of nodes containing identical copies of a shard to maintain redundancy and load balancing. |
| **Single Point of Failure (SPOF)** | A critical component whose failure stops the entire system from functioning.          |

---

# ✨ Key Concepts for Distributed Query Processing

- Queries are decomposed into distributed transactions executed across nodes.
- Must handle concurrency, deadlocks, and recovery to maintain integrity.
- Applications remain unaware of data fragmentation or replication details.

---

# ⛓️ Transaction Management Note

- ACID and BASE principles govern transaction consistency in distributed databases.
- Replication requires concurrency control mechanisms to avoid inconsistency during updates.

---

This guide covers all essential concepts, characteristics, storage approaches, fragmentation methods, sharding types, replication, and transactional considerations discussed in the lecture transcript for MEM 6287 Advanced Data Analytics Week 2b.

## 🗄️ Database Transaction Management

> "A database transaction symbolizes a unit of work performed within a database management system."

- A **transaction** represents a change to the state of a database.
- Transactions must be **managed coherently and reliably**, independently of each other.
- During execution, the database may temporarily be in an **inconsistent state** but must return to a **consistent state** after the transaction completes.

### State Transitions in Transactions

| Stage                  | Description                                           |
|------------------------|-------------------------------------------------------|
| Begin Transaction      | Marks the start of a transaction                       |
| Execution of Transaction | Operations like INSERT, UPDATE, DELETE occur         |
| Intermediate States    | Database may be inconsistent temporarily               |
| End Transaction (COMMIT)| Transaction is finalized; database returns to consistency |

---

## 🔑 ACID Properties of Transactions

| Property   | Description                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------|
| **Atomicity**  | The entire transaction either **succeeds completely** or **gets rolled back** entirely.              |
| **Consistency**| The transaction **cannot leave the database in an inconsistent state** after execution.              |
| **Isolation**  | Transactions are **isolated**; they cannot interfere with each other during execution.               |
| **Durability** | Once a transaction is committed, its results **persist permanently**, even if servers restart.      |

### Additional ACID Characteristics

- Guarantees **strong consistency** and **isolation**.
- Focuses on successful **commit** of transactions.
- Supports **nested transactions**.
- Challenges include **scaling** and **difficult schema evolution** (fixed schemas).
- Emphasizes high **availability** but can be problematic in distributed environments.

---

## ⚖️ BASE Transaction Management Model

BASE stands for:

| Letter       | Meaning                         | Description                                     |
|--------------|--------------------------------|-------------------------------------------------|
| **B**        | Basic Availability             | The system guarantees that **some version** of the data is available. |
| **A**        | Soft-State                    | The system state may change over time, even without input (e.g., replication delays). |
| **SE**       | Eventual Consistency          | The system guarantees that, **eventually**, all nodes will be consistent. |

### BASE Characteristics

- **Weak consistency** is acceptable; stale data is tolerated.
- Prioritizes **availability** over strict consistency.
- Delivers **best-effort** results, allowing **approximate answers**.
- Facilitates **scaling** and **faster** operations.
- Allows **easier schema evolution** (no fixed schema).

---

## 🔄 Concurrency Control in Transactions

- In distributed databases, **changes to resources** must be synchronized across multiple users.
- **RDMS** (Relational Database Management Systems) aim to maintain **isolation**: only committed transactions are visible.
- Distributed databases emphasize **availability**: data may be read before being committed across all nodes.
- Managing **transaction locks** is difficult in distributed systems due to synchronization challenges.

| Approach | Focus                         | Trade-off                                |
|----------|-------------------------------|-----------------------------------------|
| ACID     | Best isolation and consistency| May sacrifice availability              |
| BASE     | Best availability             | May tolerate lower consistency          |

---

## 📊 Data Validation Approaches

### Schema-on-Write

> "Validate data against a defined schema before ingestion."

- Data is checked against a schema **before being written** to the database.
- If validation fails, data ingestion is rejected.
- Ensures **high data quality**.
- The process is **slow** and **error-prone**.
- Commonly used in **RDBMS**.

**Process Flow:**

| Step          | Description                   |
|---------------|-------------------------------|
| Collect Data  | Acquire data for ingestion    |
| Apply Schema  | Validate data before writing  |
| Write Data    | Store validated data          |
| Analyze       | Perform analysis on valid data|

---

### Schema-on-Read

> "Data is written quickly without schema validation; schema is applied during read."

- Data is ingested **without any validation**.
- Suitable for **semi-structured, unstructured**, or frequently changing structured data.
- May result in **reduced data quality** (missing or invalid data, duplicates).
- Enables **fast and less error-prone** storage.
- Most **distributed databases** use this approach.

**Process Flow:**

| Step          | Description                   |
|---------------|-------------------------------|
| Collect Data  | Acquire data for ingestion    |
| Write Data    | Store raw data immediately    |
| Apply Schema  | Validate data at read time    |
| Analyze       | Analyze data after schema application|

---

## 🔺 CAP Theorem

> "In the event of a network failure, a distributed system can guarantee only two of the three: Consistency, Availability, and Partition Tolerance."

| Term              | Definition                                                                                 |
|-------------------|--------------------------------------------------------------------------------------------|
| **Consistency**   | All reads receive the **most recent write** or an error.                                 |
| **Availability**  | All reads return **some data**, but it might not be the most recent.                      |
| **Partition Tolerance** | The system continues to operate despite **network failures** partitioning nodes.         |

### Notes:

- Distributed databases **must provide Partition Tolerance**.
- They **may sacrifice either Availability or Consistency** depending on design.
- The **Consistency** in CAP differs from ACID's consistency:
  - CAP consistency means **up-to-date data for all reads across nodes**.
  - ACID consistency means **transactions do not corrupt the database during writes**.

---

## 📌 CAP Characteristics in Distributed Databases

| Characteristic       | Description                                                                                       |
|---------------------|---------------------------------------------------------------------------------------------------|
| **Partition Tolerance (HIGH)** | When a node fails, only that partition is affected; replication prevents data loss.        |
| **Data Availability (HIGH)**    | Systems aim for near 100% uptime; some reads might return stale data during updates.      |
| **Data Consistency (LOW)**      | Achieving all nodes seeing the same data simultaneously is hard; consistency is often delayed.|

---

## ⚠️ Challenges with Distributed Databases

| Challenge               | Explanation                                              |
|-------------------------|----------------------------------------------------------|
| Architectural Complexity| Building and maintaining distributed systems is complex.|
| Cost                    | Higher infrastructure and maintenance costs.             |
| Security                | Protecting data across multiple nodes increases risks.   |
| Integrity Control       | Ensuring data correctness and consistency is difficult.  |
| Lack of Standards       | Few universally accepted standards exist.                |
| Database Design Complexity | Designing schemas and queries for distributed environments is challenging. |

---

## 📚 References

- Turban and Volonino, *Information Technology for Management*, 8th edition, 2011.
- Corbett et al., *Spanner: Google’s globally distributed database*, ACM TOCS, 2013.
- Rabelo & Davis Jr., *SODDA - Service-Oriented Distributed Database Architecture*, 2008.
- Web Articles:
  - CAP Theorem: https://www.bmc.com/blogs/cap-theorem/
  - Types of NoSQL Databases: https://www.dataversity.net/nosql-data-architecture-data-governance-everything-need-know/
  - Schema on Read vs. Schema on Write: https://luminousmen.com/post/schema-on-read-vs-schema-on-write
  - Database Sharding: https://levelup.gitconnected.com/what-is-database-sharding-and-how-is-it-done-f36b9cb653e8
  - Distributed Query Design: https://cs.uwaterloo.ca/~tozsu/ddbook/downloads/presentations/6-Query_Intro.pptx
  - Distributed Databases (University of Southampton): http://edshare.soton.ac.uk/19880/1/13%20-%20Distributed%20Databases.pptx
  - Database Replication: https://searchdatamanagement.techtarget.com/definition/database-replication