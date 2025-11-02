## 📊 Types of NoSQL Databases

| Type               | Description                                                                                  | Examples                          | Key Features                                               |
|--------------------|----------------------------------------------------------------------------------------------|---------------------------------|------------------------------------------------------------|
| **Key-Value Stores**      | Store data as maps of key-value pairs; schema-less; values can be any data type including documents. | Redis, DynamoDB, Memcached       | Simple structure, schema-less, fast lookups.                |
| **Document-Based Stores** | Store data as documents (JSON or BSON); schema-agnostic; documents have unique keys; heterogeneous.  | MongoDB, CouchDB, Azure Cosmos DB | Flexible, hierarchical data storage, easy to query documents. |
| **Column-Oriented Stores**| Store data in column families; data is key/value pairs identified by a row-key, ordered and sorted by row-key. | Cassandra, Google Bigtable, HBase | Optimized for large-scale, distributed storage.             |
| **Graph Databases**       | Store data as nodes and edges with attributes; labeled nodes/edges for efficient relationship queries. | Neo4j, OrientDB, ArangoDB        | Ideal for relationship-intensive data like social networks. |

---

## ⚙️ Common Characteristics of NoSQL Databases

- **Schema-less:** Handle semi-structured or unstructured data.
- **Distributed & Clustered:** Designed for horizontal scalability through clustering.
- **High Performance:** Often faster than traditional RDBMS, suitable for Big Data.
- **Transaction Model:** Typically support BASE transactions (Basically Available, Soft state, Eventual consistency) rather than strict ACID.

---

## 🧩 CAP Theorem & NoSQL Databases

- NoSQL databases balance **Consistency, Availability, and Partition tolerance**.
- Often trade off strict consistency for better availability and partition tolerance.

---

## 🗝️ Key/Value Store Details

- Store data as key-value pairs without schema constraints.
- Values can be documents or any data type.
- Use cases include caching and real-time applications.
- Example usage: Redis used by Instagram, Stack Overflow, and Flickr.

---

## 📄 Document-Based Databases

> *"Unlike RDMS which uses records as units of storage, document databases use documents in JSON or BSON format."*

- Documents have a unique key.
- Documents are schema-agnostic and heterogeneous.
- APIs or query languages retrieve documents based on queries.
- Example databases: MongoDB, Apache CouchDB, MS Azure Cosmos DB.

---

## 🗃️ Column-Oriented Stores

| Feature                    | Description                                                       |
|----------------------------|-------------------------------------------------------------------|
| Data storage               | Groups data into column families                                   |
| Unit of data               | Set of key/value pairs identified by a row-key                    |
| Ordering                   | Data sorted by row-key                                            |
| Examples                   | Cassandra, Google Bigtable, HBase                                 |
| Typical use cases          | Big data analytics, time series, and large-scale distributed apps |

---

## 🔗 Graph Databases

- Store data as **nodes** (entities), **edges** (relationships), and **attributes**.
- Nodes and edges can have labels and multiple attributes.
- Labels help narrow down searches.
- Example applications: social media graphs, transportation networks.
- Popular graph DBs: Neo4j, OrientDB.

---

## 🏗️ MongoDB Architecture

- Document-oriented NoSQL database designed for **high-volume data storage**.
- Uses **collections** (similar to tables) and **documents** (similar to rows).
- Documents stored in **Binary JSON (BSON)** format.
- Supports **auto-sharding** for horizontal scaling and **replication** for load balancing and fault tolerance.

**MongoDB Cluster Components:**

| Component      | Role                                    |
|----------------|-----------------------------------------|
| Mongod         | Database server handling data storage   |
| Mongos         | Query router for sharded clusters       |
| Config Server  | Stores metadata and cluster configuration |
| Shards         | Data partitions distributed across servers |

---

## 🗃️ MongoDB Database & Documents

- Databases contain **collections**.
- Collections contain **documents** with a max size of 16MB.
- Documents are collections of field-value pairs stored as BSON.
- Supports all JSON types: int, long, double, string, object, array, bool, date, regex, null.
- Allows **embedded documents** (nested objects).
- Each document requires a unique `_id` as a primary key.

---

## 💻 MongoDB Query Model

- Supports multiple programming languages (Java, .NET, Ruby, Python, etc.).
- Provides **Mongo Shell** (JavaScript shell) and **MongoDB Compass** (GUI).
- Query types supported:
  - Key-value queries
  - Range queries
  - Geospatial queries
  - Text search
  - Aggregate framework queries
  - Map-reduce queries
  - Aggregation pipelines
- Secondary indexes can be created on any document field.
- MongoDB is **ACID-compliant at the document level**, ensuring consistency per document.

---

## 🔄 Differences Between MongoDB and RDBMS

| Feature               | MongoDB                                  | RDBMS                                      |
|-----------------------|-----------------------------------------|--------------------------------------------|
| Data Model            | Document-oriented, non-relational       | Relational, table-based                     |
| Schema                | Dynamic schema, supports hierarchical data | Fixed schema, less suited for hierarchy    |
| Setup Complexity      | Relatively easy                         | More complex                               |
| Security              | Unaffected by SQL injection             | Vulnerable to SQL injection                 |
| Performance & Scaling | 100x faster, horizontally scalable      | Vertical scaling by increasing RAM         |

---

## 📝 Important MongoDB Features

| Feature              | Description                                   |
|----------------------|-----------------------------------------------|
| Queries              | Support ad-hoc and document-based queries     |
| Indexing             | Indexes can be created on any field            |
| Replication          | Master-Slave replication model                  |
| Horizontal Scaling   | Supports multi-server deployment, auto-sharding, load balancing |
| Big Data Analytics   | Supports MapReduce and Aggregation Pipelines   |
| Schema-less          | No enforced schema, flexible data structure    |
| GridFS               | Storage for large files                          |

---

## 🔍 MongoDB Query Components

| Component   | Description                                             |
|-------------|---------------------------------------------------------|
| Filter      | Conditions to select documents                           |
| Projection  | Select specific fields (document attributes)            |
| Sort        | Order documents by specified fields                      |
| Skip        | Number of documents to skip in the result set           |
| Limit       | Number of documents to return                             |

---

## 🔄 Document vs. Tabular Views in MongoDB

- **Document View:** Displays hierarchical JSON-like documents.
- **Tabular View:** Flattens the document into table-like rows and columns.

---

## 📊 MongoDB Filtering Operators

| Operator          | Example Query                                | Description                        |
|-------------------|---------------------------------------------|----------------------------------|
| **OR**            | `{$or: \lbrack {"borough": "Brooklyn"}, {"cuisine": "Japanese"}\rbrack }` | Logical OR between conditions     |
| **Equal ($eq)**   | `{borough: {$eq: "Brooklyn"}}`               | Matches exact value                |
| **Not Equal ($ne)**| `{borough: {$ne: "Brooklyn"}}`                | Excludes the specified value      |
| **Not In ($nin)** | `{borough: {$nin: \lbrack "Brooklyn", "Queens"\rbrack }}`  | Excludes values in the list        |
| **Contains**      | `{name: /Deli/}`                              | Matches substring in field        |
| **Starts With**   | `{name: /^Deli/}`                             | Matches fields starting with text |
| **Ends With**     | `{name: /Deli$/}`                             | Matches fields ending with text   |
| **Greater Than ($gt)** | `{bytesIn: {$gt: 500000}}`               | Matches values greater than given |

---

## 📚 Summary of MongoDB Query Example

- Select fields: `name`, `description`, `minimum_nights` (hide `_id`).
- Sort results by `name`.
- Query documents where `minimum_nights` equals 4.
- More complex sorting and filtering can use operators and ranges.

---

## 🗂️ MongoDB Data Storage Model vs RDMS

| Model        | Description                                                                                  |
|--------------|----------------------------------------------------------------------------------------------|
| RDMS Model   | Uses multiple relational tables joined by keys                                              |
| MongoDB Model| Stores each entity as a document (e.g., one document per TV show); avoids JOINs for faster read |

- Query performance is optimized by avoiding expensive JOIN operations.
- Document scans may degrade performance if queries are not selective.

---

# End of Lecture Content

## 🗂️ MongoDB Query Optimization and Indexing

> **Indexes** in MongoDB serve to limit the number of documents scanned during a query, improving performance significantly compared to a full collection scan.

### Index Basics

| Concept                | Description                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------|
| Collection Scan        | Default query behavior without indexes; scans all documents.                                     |
| Index Usage            | Uses indexes to filter documents, reducing the scan size and improving query speed.              |

### Creating Indexes

```js
db.collection.createIndex(<key and index type specification>, <options>)
```

- **Example 1:** Index on `name` field in descending order:
  ```js
  db.collection.createIndex({ name: -1 })
  ```
- **Example 2:** Named compound index on `item` (ascending) and `quantity` (descending):
  ```js
  db.products.createIndex(
    { item: 1, quantity: -1 },
    { name: "query for inventory" }
  )
  ```

### Supported Index Types

| Index Type         | Description                                                       |
|--------------------|-------------------------------------------------------------------|
| **_id Index**      | Default index on document ID.                                     |
| **Simple Index**   | Index on a single field.                                          |
| **Compound Index** | Index on multiple fields.                                         |
| **Multikey Index** | Indexes fields containing arrays.                                |
| **Geospatial Index**| Enables efficient queries on geospatial coordinates.             |
| **Text Indexes**   | Supports string content search within a collection.              |

---

## ⚡ Covered Queries

> When both the **query filter** and **projection** use only indexed fields, MongoDB returns results directly from the index without scanning documents, making these queries extremely efficient.

---

## 📝 CRUD Operations in MongoDB

### Insert Operations

| Operation Type          | Command                      | Description                     |
|------------------------|-----------------------------|---------------------------------|
| Single Document Insert | `db.collection.insertOne()` | Adds one document to the collection. |
| Multiple Document Insert| `db.collection.insertMany()`| Adds multiple documents at once. |

### Update Operations

| Operation Type             | Command                   | Description                                  |
|---------------------------|---------------------------|----------------------------------------------|
| Single Document Update     | `db.collection.updateOne()`| Updates one document matching a filter.      |
| Multiple Document Update   | `db.collection.updateMany()`| Updates multiple documents matching a filter.|
| Replace One Document       | `db.collection.replaceOne()`| Replaces a document matching a filter.       |
| Generic Update            | `db.collection.update()`    | Performs generic update operations.           |

### Delete Operations

| Operation Type           | Command                  | Description                              |
|-------------------------|--------------------------|------------------------------------------|
| Single Document Delete   | `db.collection.deleteOne()`| Deletes one document matching a filter. |
| Multiple Document Delete | `db.collection.deleteMany()`| Deletes multiple documents matching a filter. |
| Remove                  | `db.collection.remove()`  | Removes documents (deprecated in favor of delete commands). |

---

## 🛠️ Bulk Write

> MongoDB supports **bulk write operations** to execute multiple changes (inserts, updates, deletes) in a single batch, improving efficiency.

---

## 🔄 Map-Reduce Framework

| Stage   | Description                                          |
|---------|------------------------------------------------------|
| **Query** | Supplies data for the map stage.                    |
| **Map**   | Projects fields for processing.                     |
| **Reduce**| Performs aggregation or special operations on mapped fields. |
| **Output**| Displays the final results.                          |

> **Note:** Aggregation Pipeline is preferred over Map-Reduce for better performance and usability.

---

## 📊 Aggregation Pipeline

> Aggregation pipelines process and group data records, performing operations to return computed results.

### Supported Aggregation Types

| Type                          | Description                                         |
|-------------------------------|-----------------------------------------------------|
| Aggregation Pipeline           | Multi-stage data processing pipeline.               |
| Map-Reduce Function            | Custom map and reduce operations.                    |
| Single-Purpose Aggregation Ops | Built-in, one-step aggregation commands.             |

### Common Pipeline Stages

| Stage    | Function                                               |
|----------|--------------------------------------------------------|
| **$match** | Filters documents based on criteria and passes them to the next stage. |
| **$group** | Groups documents by specified field and performs calculations on groups. |

---

## 🔢 Single-Purpose Aggregation Methods

| Method                           | Description                          |
|---------------------------------|------------------------------------|
| `db.collection.estimatedDocumentCount()` | Returns an estimated count of documents. |
| `db.collection.count(<field>)`              | Returns count of values for a field. |
| `db.collection.distinct(<field>)`           | Returns a list of distinct values for a field. |

---

## 🔄 MongoDB Replication

> Replication provides **fault tolerance** and **high availability** by maintaining copies of data across multiple servers (replica set).

### Replica Set Components

| Component         | Role                                                                 |
|-------------------|----------------------------------------------------------------------|
| **Primary Node**  | Receives all write operations and records changes in the operation log (`oplog`). |
| **Secondary Nodes**| Replicate `oplog` from primary and apply updates locally.            |

### Fault Tolerance Mechanism

- If the **primary node fails**, secondary nodes hold an **election** to choose a new primary.
- **Arbiter:** A special MongoDB instance that participates in elections but holds no data.
- Nodes can transition roles: primary ↔ secondary.

---

## 🗃️ MongoDB Sharding for Horizontal Scaling

> Sharding allows MongoDB to horizontally scale by distributing data across multiple servers (shards).

### Benefits and Trade-offs

| Benefit                                   | Trade-off                             |
|-------------------------------------------|-------------------------------------|
| Expands capacity by adding servers.       | Increases infrastructure complexity. |
| Supports very large datasets and high throughput. | Requires managing shard keys and chunk distribution. |

### Sharded Cluster Components

| Component       | Description                                                      |
|-----------------|------------------------------------------------------------------|
| **Shard**       | Contains a subset of the data; often deployed as a replica set. |
| **mongos**      | Router providing interface between clients and sharded cluster. |
| **Config Servers**| Store metadata and configuration for the cluster; usually a replica set. |

### Key Sharding Concepts

- Shard key: Field used to partition the collection across shards.
- Collections are split into **chunks** based on shard key ranges.
- Chunks are distributed and replicated across shards.

---

## 🧪 MongoDB Lab Setup

- Use **MongoDB Atlas** (https://www.mongodb.com/cloud) for cloud-based MongoDB instances.
- Free account offers up to 500 MB storage, supports group participation, multiple databases, and collections.
- Use **MongoDB Compass** (https://www.mongodb.com/products/compass) for GUI-based management.

---

## ⚠️ MongoDB Limitations

| Limitation                            | Explanation                                      |
|-------------------------------------|-------------------------------------------------|
| Max BSON document size: 16MB         | Limits document size; use **GridFS** for larger files. |
| Max BSON nesting levels: 100         | Limits document depth to avoid excessive complexity. |
| Max indexes per collection: 64       | Limits the number of indexes.                    |
| Storage limits                      | 4 TB on Windows, 64 TB on Linux per instance.   |
| Replica set nodes: max 12             | Maximum nodes per replica set.                   |
| Voting nodes in replica set: max 7   | Maximum voting nodes allowed.                     |
| Max connections: 20,000              | Hardcoded connection limit.                       |

---

## References for Further Study

| Topic                     | URL                                                                    |
|---------------------------|------------------------------------------------------------------------|
| MongoDB Architecture      | https://docs.mongodb.com/manual/storage/                               |
| Introduction to MongoDB Queries | https://blog.exploratory.io/an-introduction-to-mongodb-query-for-beginners-bd463319aa4c |
| CRUD Operations           | http://man.hubwiz.com/docset/MongoDB.docset/Contents/Resources/Documents/docs.mongodb.org/manual/core/write-operations-introduction/index.html |
| Aggregation Pipelines     | https://www.practical-mongodb-aggregations.com/                        |