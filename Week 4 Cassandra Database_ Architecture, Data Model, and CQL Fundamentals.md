## 📚 Cassandra Architecture and Data Model

### Cassandra Overview

- **Cassandra** is a **column-oriented, distributed, fault-tolerant, and linearly scalable** NoSQL database.
- It handles **large volumes of **`structured and semi-structured`** data**.
- Uses distributed storage that **scales linearly** by adding commodity servers.
- Supports **multi-data center and multi-region deployments**.
- Has **no single point of failure**.
- Offers **tunable consistency** adjustable per application needs.
- Uses **Cassandra Query Language (CQL)**, which has SQL-like syntax.
- Supports **Java Monitoring Extensions (JMX)** for performance and latency metrics.

---

### NoSQL Databases Key Characteristics

| Characteristic | Description |
| --- | --- |
| Schema-less | Data is semi-structured or unstructured, no fixed schema. |
| Distributed & Clustered | Supports horizontal scaling across nodes in a cluster. |
| Performance | Typically better performance than relational databases for big data and real-time analytics. |
| Transaction Model | Mostly BASE transactions (Basically Available, Soft state, Eventual consistency), not ACID. |
| Types of NoSQL Databases | Key-value store, Document store, Column-based store, Graph-based store. |

**Examples of NoSQL Databases:**

| Type | Examples |
| --- | --- |
| Key-Value Store | Redis, DynamoDB, Memcached |
| Document Store | MongoDB, CouchDB, Amazon Document DB, Cosmos DB |
| Column Store | Cassandra, HBase, BigTable |
| Graph Store | Neo4J, OrientDB, GraphDB, ArangoDB |

---

### Cassandra Data Model Components

| Cassandra Term | Relational Database Equivalent |
| --- | --- |
| Keyspace | Database |
| Column Family | Table |
| Partition Key | Primary Key (partition component) |
| Clustering Columns | Columns used to sort data within a partition |
| Column Name | Column Name |
| Row | Row |

---

### Data Partitioning in Cassandra

- Data is organized into **partitions**, each stored on a single node.
- **Partition key** determines how data is distributed across nodes.
- The **primary key** consists of the partition key plus optional clustering columns:

$$\text{Primary Key} = \text{Partition Key} + \lbrack \text{Clustering Columns}\rbrack$$

- Cassandra hashes the partition key to assign data to nodes.
- Even data distribution is critical; partitions should be balanced across nodes.
- Data duplication is common due to the **lack of join operations** across partitions.
- **Clustering columns** sort data within a partition (ascending by default).

---

### Cassandra Node Characteristics

- Each node is a **fully independent database**.
- Uses **in-memory or persistent storage**.
- **Fast writes** via durable write-to-log files without locking or reading DB files.
- **Fast reads** retrieve data from memory first with no locking.
- Nodes form a **peer-to-peer cluster** with built-in replication and failure avoidance.

---

### Replication and Partition Key Distribution

- Cassandra replicates data based on the **replication factor**.
- Data for a partition key is stored on one node and **replicated clockwise** to sibling nodes.
- Example replication for partition keys 23 and 88 (range 0-99):

| Partition Key | Primary Node | Replicated Nodes |
| --- | --- | --- |
| 23 | Node 1 | Node 2, Node 3 |
| 88 | Node 4 | Node 1, Node 2 |

---

### Deployment Scenarios

- Supports **multi-region and multi-data center replication**.
- Rows can have **Time-to-Live (TTL)** settings for automatic expiration.
- **Coordinator node** manages client requests, acting as a proxy to other nodes.
- Coordinator responsibilities:

    - Manages request path.
    - Sends responses back to clients.- In multi-DC setups, remote coordinators handle cross-data center requests.

---

## ⚙️ Tunable Consistency in Cassandra

- Tunable consistency allows adjusting **consistency level per read/write operation**.
- Balances **consistency, availability, latency, and throughput**.
- Common consistency levels from low consistency to high consistency:

| Consistency Level | Description |
| --- | --- |
| ONE | Operation succeeds if at least one replica responds. |
| LOCAL_QUORUM | Quorum of replicas in the same data center. |
| QUORUM | Operation succeeds if a majority of replicas respond. |
| EACH_QUORUM | Quorum of replicas in every data center. |
| ALL | Operation succeeds only if all replicas respond. |



- **QUORUM** is calculated as:

$$\text{QUORUM} = \left(\frac{\text{replication factor}}{2}\right) + 1$$

- Use cases:

| Scenario | Recommended Consistency Level |
| --- | --- |
| Strong consistency | QUORUM |
| High availability | ONE |
| Multi-datacenter | LOCAL_QUORUM |

---

## 📊 Example of Data Partitioning and Primary Key Structure

Example sensor data table:

| Sensor # | Date | Timestamp | Metric 1 | Metric 2 | Metric 3 |
| --- | --- | --- | --- | --- | --- |
| 1 | 2015-01-01 | 20150101-000000 | 5.01 | 5.67 | 0.678 |
| 1 | 2015-01-01 | 20150101-000010 | 5.01 | 5.67 | 0.678 |
| ... | ... | ... | ... | ... | ... |
| 2 | 2015-01-02 | 20150102-000000 | 6.01 | 7.67 | 0.978 |

- **Primary key**:

$$\text{PRIMARY KEY} ((\text{Sensor}, \text{Date}), \text{Timestamp})$$

- **Partition key**: composite key of (Sensor, Date).
- **Clustering key**: Timestamp, which orders rows within the partition.

---

## 🛠️ Defining Tables and Keys in Cassandra CQL

### Table Definitions and Keys

| Table Name | Partition Key | Clustering Columns | Notes |
| --- | --- | --- | --- |
| `server_logs_by_hour` | `log_hour` | None | Single column primary key = partition key |
| `server_logs_by_hour_level` | `log_hour` | `log_level` | Clustering column sorts data within partition |
| `server_logs_by_hour_server` | `(log_hour, server)` composite key | None | Composite partition key |
| `server_logs_by_hour_server` | `(log_hour, server)` composite key | `log_level` | Clustering column with descending sort order |

- The **partition key** distributes data across cluster nodes.
- When primary key has one column, it is the partition key.
- **Clustering columns** sort data inside a partition (ascending by default unless specified).
- Composite keys are made of multiple columns to better distribute large datasets.

---

## 🔑 Composite Keys in Cassandra

- Composite keys consist of **multiple columns** as the partition key.
- Necessary when a single column cannot fit all data into one partition.
- Example: storing all gyms in a country may require composite keys for better distribution.

---

# Key Takeaways

- Cassandra is designed for **horizontal scalability and fault tolerance** with no single failure point.
- It uses a **partition key to distribute data and clustering columns to order data within partitions**.
- **Replication factor** controls data redundancy and fault tolerance.
- **Tunable consistency** allows balancing between consistency and availability.
- **Composite keys** and data modeling must consider even data distribution and read/write efficiency.

## 🗝️ Composite Partition Keys and Query Requirements

- For large countries, use **composite keys** including `state` and `city` to create partitions that fit into a node.
- The **partition key** is part of the **primary key** and defines how data is distributed across nodes.
- Each partition key component corresponds to a separate partition within the cluster.
- **All queries must include all partition key columns at minimum** to be valid.

### Example Table: `crossfit_gyms_by_country_province_city`
```sql
CREATE TABLE crossfit_gyms_by_country_province_city (
  country_code text,
  state_province text,
  city text,
  gym_name text,
  PRIMARY KEY ((country_code, state_province, city), opening_date, gym_name)
) WITH CLUSTERING ORDER BY (opening_date ASC, gym_name ASC);
```
### Valid Queries Examples

| Query | Validity |
| --- | --- |
| `SELECT * FROM crossfit_gyms_by_country_province_city WHERE country_code='USA' and state_province='VA'` | Valid |
| `SELECT * FROM crossfit_gyms_by_country_province_city WHERE country_code='USA' and state_province='VA' and city='Arlington' and gym_name='CrossFit Route 7'` | Valid |
| `SELECT * FROM crossfit_gyms_by_country_province_city WHERE country_code='USA' and state_province='VA' and city='Arlington'` | Valid |
| `SELECT * FROM crossfit_gyms_by_country_province_city WHERE country_code='USA' and state_province='VA' and city='Arlington' and opening_date < '2015-01-01 00:00:00+0200'` | Valid |

### Invalid Queries

- Any query missing one or more partition key components (`country_code`, `state_province`, `city`) is invalid.

---

## 📊 CQL ORDER BY Clause

- Sorting is specified using the **WITH CLUSTERING ORDER BY** clause in the `CREATE TABLE` statement.
- You **must specify the sort order for each clustering key**.
- The **partition key is not part of the ORDER BY** clause because partition keys are hashed and thus not sorted within the cluster.

### Example Table with ORDER BY
```sql
CREATE TABLE crossfit_gyms_by_location (
  country_code text,
  state_province text,
  city text,
  gym_name text,
  PRIMARY KEY (country_code, state_province, city, gym_name)
) WITH CLUSTERING ORDER BY (state_province DESC, city ASC, gym_name ASC);
```
| Key Type | Included in ORDER BY? | Reason |
| --- | --- | --- |
| Partition Key | No | Partition keys are hashed, no ordering inside partition |
| Clustering Keys | Yes | Ordering can be defined per clustering key |

---

## 🗃️ Cassandra Support for Heterogeneous Data Types

Cassandra can internally store and manage **maps**, **lists**, and **sets** in columns.

| Data Type | Storage Mechanism | Column Naming Convention | Value Storage |
| --- | --- | --- | --- |
| **Map** | Adds a column for each item; column name = `column_name:map_key` | e.g., `map1:patricia` | Value is the map key's value |
| **List** | Adds a column for each list entry; column name = `column_name:UUID` (UUID generated by Cassandra) | e.g., `list1:26017c10f48711e2801fdf9895e5d0f8` | Value is the list item |
| **Set** | Adds a column for each set entry; column name = `column_name:entry_value` | e.g., `set1:'patricia'` | Value is empty (stored in the column name) |

### Example Table and Insert
```sql
CREATE TABLE example (
  key1 text PRIMARY KEY,
  map1 map<text,text>,
  list1 list<text>,
  set1 set<text>
);

INSERT INTO example (key1, map1, list1, set1) VALUES (
  'john',
  {'patricia':'555-4326', 'doug':'555-1579'},
  ['doug', 'scott'],
  {'patricia', 'scott'}
);
```
### Resulting Row Columns

| Column | Value | Notes |
| --- | --- | --- |
| (root column) | (empty) | Row key: `john` |
| `map1:doug` | `555-1579` | Map entry for key `doug` |
| `map1:patricia` | `555-4326` | Map entry for key `patricia` |
| `list1:26017c10f48711e2801fdf9895e5d0f8` | `doug` | List entry with UUID suffix |
| `list1:26017c12f48711e2801fdf9895e5d0f8` | `scott` | List entry with UUID suffix |
| `set1:'patricia'` | (empty) | Set entry stored in column name |
| `set1:'scott'` | (empty) | Set entry stored in column name |

---

## 🛠️ Important CQL Commands

| Command | Usage Example | Description |
| --- | --- | --- |
| **describe** | `describe keyspaces;`   `describe table <tablename>;` | Describes Cassandra cluster objects |
| **expand** | `expand on;`   `expand off;` | Toggles expanded output display |
| **create** | `CREATE KEYSPACE tutorialspoint WITH replication = {'class':'SimpleStrategy', 'replication_factor' : 3};`    `CREATE TABLE <tablename> ...;` | Creates keyspaces and tables |
| **drop** | `drop keyspace <keyspacename>;`   `drop table <tablename>;` | Removes keyspaces or tables |

---

## 📝 Important CQL CRUD Commands

| Operation | Syntax Example | Notes |
| --- | --- | --- |
| **SELECT** | `SELECT [fields] FROM <table> WHERE <partition_key_and_optional_cluster_keys>;` | The `WHERE` clause **must include all partition key columns** and optionally clustering keys |
| **INSERT** | `INSERT INTO <table_name> VALUES ([list_of_values]);` | Adds a new record |
| **UPDATE** | `UPDATE <table_name> SET field=value, ... WHERE <condition>;` | Updates an existing record |
| **DELETE** | `DELETE FROM <table_name> WHERE <condition>;` | Deletes an existing record |

---

## ⚡ Cassandra Characteristics

| Characteristic | Description |
| --- | --- |
| Extremely fast query reads/writes | Optimized for speed in both operations |
| Data duplication encouraged | Improves read efficiency through denormalization |
| Fast write performance | Optimized for write-heavy workloads |
| High throughput for both reads and writes | Handles large volumes of data seamlessly |
| Linear scalability | Add commodity servers to scale horizontally |
| Multi-region and multi-data center replication | Supports global data distribution |
| Time-to-live (TTL) support | Can set expiration time on each record |
| High availability | No single point of failure ensures continuous operation |
| Tunable consistency | Consistency levels can be adjusted per operation |

---

## ⚠️ Cassandra Limitations

| Limitation | Explanation |
| --- | --- |
| Limited ACID support | Cassandra does not fully support Atomicity, Consistency, Isolation, Durability |
| Writes and deletes degrade query performance | Frequent deletions can impact read efficiency |
| Potential for stale reads at low consistency | Low read consistency may return outdated data |
| No support for JOINs or subqueries | Requires denormalization; no cross-partition joins |
| Ordering set at table creation per partition | Cannot sort billions of rows on the client side dynamically |
| Single partition must fit on one node | Partition size should be < 100MB and < 100k rows |
| Single-column value size limited to 2GB | Maximum allowed size for a single column value |

---

## 💻 Cassandra Lab

- Use **DataStax Astra Cassandra-as-a-Service**: https://astra.datastax.com/
- Provides an account with $25 credit for practice (paid service).
- Setup your account to practice Cassandra queries and data modeling.

---

## 📚 References

- Cassandra Modeling & Query Best Practices:

    - https://medium.com/@herryg91/in-depth-why-modeling-in-cassandra-is-important-ba25081dafd5
    - https://www.red-gate.com/simple-talk/sql/nosql-databases/apache-cassandra-data-modeling-and-query-best-practices/
    - https://shermandigital.com/blog/designing-a-cassandra-data-model/- MongoDB Documentation & Guides:

    - https://docs.mongodb.com/manual/storage/
    - https://intellipaat.com/blog/what-is-mongodb/
    - https://jira.mongodb.org/secure/attachment/112939/MongoDB_Architecture_Guide.pdf
    - https://blog.exploratory.io/an-introduction-to-mongodb-query-for-beginners-bd463319aa4c
    - http://man.hubwiz.com/docset/MongoDB.docset/Contents/Resources/Documents/docs.mongodb.org/manual/core/write-operations-introduction/index.html
    - https://www.practical-mongodb-aggregations.com/
