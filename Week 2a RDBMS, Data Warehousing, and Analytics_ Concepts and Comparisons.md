## 🔍 Traditional Data Processing Constructs in RDBMS

> **Relational Database (RDBMS):** A collection of logically related data organized to meet an organization's information needs.

- **Database Management System (DBMS):** Software that manages database objects and their relationships (e.g., Oracle, SQL Server).
- **Application Programs:** Interact with the database by issuing requests to the DBMS.
- Example: Human Resources Database includes Employees, Payroll, Benefits data accessed by respective departmental applications.

### Data Validation Using Schemas

> **Schema:** A set of rules that govern a database, written in data definition languages like SQL, JSON Schema, or XML DTD.

- Defines validation rules for attributes, data formats, and relationships.
- Created by database designers via **data modeling**.
- In RDBMS, schemas are often represented through **Entity-Relationship (E/R) diagrams**.
- Different handling of schema in distributed databases.

### Entity-Relationship Diagram (ERD) in RDBMS

- Visual representation of entities, attributes, and relationships.
- Helps to design normalized schemas.

---

## 🛠️ Querying and Operations in Relational Databases

### SQL Basics

- **SQL (Structured Query Language):** Used to query, update, and manage relational databases.
  
Example SQL query selecting parts priced under $25:

```sql
SELECT Part_Number, Part_Description, Unit_Price
FROM PARTS
WHERE Unit_Price < 25.00
```

### Basic Operations

| Operation | Description                                            |
|-----------|--------------------------------------------------------|
| SELECT    | Retrieve specific columns or rows from tables          |
| JOIN      | Combine rows from two or more tables based on keys     |
| GROUP BY  | Aggregate data based on specified columns               |
| Aggregate Functions | SUM, AVG, MIN, MAX to compute summaries          |

### SQL Joins Explained

Joins combine data from multiple normalized tables to create denormalized views for analytics.

| Join Type    | Description                                               | Example Use Case                         |
|--------------|-----------------------------------------------------------|-----------------------------------------|
| INNER JOIN   | Returns rows with matching keys in both tables            | Matching orders and customers            |
| LEFT JOIN    | Returns all rows from left table, matched rows from right | All customers and their orders, if any  |
| RIGHT JOIN   | Returns all rows from right table, matched rows from left | All orders and their customers, if any  |
| FULL OUTER JOIN | Returns rows when there is a match in either table      | Complete list of customers and orders   |

Example SQL syntax for LEFT JOIN:

```sql
SELECT <select_list>
FROM TableA A
LEFT JOIN TableB B ON A.Key = B.Key
```

### Other Important SQL Statements

| Statement     | Purpose                                                |
|---------------|---------------------------------------------------------|
| GROUP BY      | Summarize and group data                                |
| Aggregate Functions | Calculate totals, averages, minimums, maximums        |
| CASE         | Provide inline conditional logic                        |
| INSERT, UPDATE, DELETE | Perform CRUD operations on data                     |

---

## ✅ Advantages of RDBMS

| Advantage           | Explanation                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| Controls Redundancy | Normalization creates atomic relations, reducing duplicate data                            |
| Data Consistency    | Updates are performed once and immediately available                                      |
| Data Sharing       | Authorized users can share data                                                              |
| Data Integrity     | Constraints enforce valid data (e.g., salary limits)                                        |
| Security           | Centralized user authentication and authorization                                          |
| Accessibility      | Cross-departmental data access                                                              |
| Data Independence  | Separation of data description from applications                                           |
| Increased Concurrency | Supports multiple simultaneous users                                                       |

---

## ⚠️ Disadvantages of RDBMS

| Disadvantage      | Explanation                                                                |
|-------------------|----------------------------------------------------------------------------|
| Complexity        | RDBMS software is complex due to extensive functionality                   |
| Cost              | Licensing and maintenance costs vary by environment and features           |
| Performance       | Performance slows down with very large data volumes                        |
| High Impact of Failure | System failure affects many users due to central dependency              |

---

## 🐘 Big Data Challenges to RDBMS

- **Vertical Scalability Limits:** RDBMS scale-up by adding more CPU, RAM, HDD but face physical limits.
- **Schema Rigidity:** Requires predefined schema including tables, columns, data types, primary/foreign keys.
- **Incompatibility with Agile:** Static schema not suitable for fast-changing, dynamic big data applications.
- **Summary:** Traditional RDBMS is poorly suited for big data workloads.

| Scaling Type   | Description                           | Example                      |
|----------------|-------------------------------------|------------------------------|
| Scale-Up (Vertical) | Adding more resources to a single machine | More RAM, CPU, HDD           |
| Scale-Out (Horizontal) | Adding more commodity hardware nodes    | Distributed systems, clusters |

---

## 📊 Problem of Analyzing Large Volumes of Data

Organizations need quick answers to questions like:

- Number of units sold per product.
- Best selling product.
- Weekly sales trends.
- Sales by location.
- Customer demographics and sales splits by gender, income, residential area.

**Challenge:** Running SQL queries on big data is expensive and slow, while executives require immediate insights.

---

## 🔄 Transactional Data vs. Analytical Information

| Type               | Characteristics                                               | Example                         |
|--------------------|---------------------------------------------------------------|---------------------------------|
| Transactional Data  | Captures day-to-day operations, high volume, normalized data | Airline ticket sales receipts    |
| Analytical Information | Summarized, historical, used for decision making            | Sales projections, growth trends |

---

## 🆚 When to Use Relational vs Non-Relational Data

| Factor             | Relational (RDBMS)                                | Non-Relational (NoSQL/Big Data)            |
|--------------------|--------------------------------------------------|--------------------------------------------|
| Data Volume        | High volume of transactions                       | High volume of data                         |
| Processing Speed   | Fast processing for transactions                  | Slower queries for analytics                |
| Data Shape        | Normalized data, many tables                       | Denormalized data, fewer tables             |
| Typical Query     | "Who bought X?" (transactional)                   | "How many people bought X?" (analytical)   |
| Application Type  | OLTP (Online Transaction Processing)               | OLAP (Online Analytical Processing)         |

---

## 📈 Online Analytical Processing (OLAP)

- **OLAP:** Tools that extract and present multi-dimensional data for strategic decision-making.
- Data is represented as a **Cube** for multiple perspectives.
- Common OLAP functions:
  - **Trend analysis**
  - **Drilling down** into detailed data
  - **Rolling up** to aggregate summaries

---

# End of Study Guide for Week 2a Lecture on RDBMS & Data Warehouse Review

## 🏢 Data Warehouse Fundamentals

> **Data Warehouse**: A copy of transaction data specifically structured for querying, analysis, reporting, and rigorous data mining. It contains a copy of transactional data that **cannot be changed** by the original transaction system after being stored.

- Data in the warehouse is often **transformed** during copying to fit analytical needs.
- It **stores data from multiple sources and over many time periods** to form a consistent and useful organizational memory.
- Helps organizations **remember and learn** from observed data.

---

## ⚙️ Characteristics of Data Warehouses

| Characteristic                          | Description                                                                                     |
|---------------------------------------|-------------------------------------------------------------------------------------------------|
| Data Version                          | Holds a version of transactional data optimized for querying and analysis.                      |
| Data Transformation                   | Data is often transformed from original transactional form through analytical processing.      |
| Historical and Current Data           | Stores both current and historical data for comprehensive analysis.                             |
| Data Integration                     | Consolidates disparate data from throughout the organization to support decision-making.       |
| Purpose                             | Primarily used for management analysis, decision support, and business intelligence.           |
| Common Technology                   | Uses RDBMS such as Oracle, DB2, SQL Server for data warehousing.                                |

---

## 🔍 Comparison: Data Warehouses vs. Databases

| Aspect                 | Databases                               | Data Warehouses                                     |
|------------------------|----------------------------------------|----------------------------------------------------|
| Data Content           | Current operations, updated in real-time with high volume. | Past and current data, updated at regular intervals (hourly, daily). |
| Query Speed            | Quick, with turnaround often in milliseconds to seconds. | Queries may take longer, including overnight processing. |
| Data Change            | Content changes frequently due to transactions and master data updates. | Content is **read-only** after loading; data can only be added, not changed. |
| Data Organization      | Optimized for online transaction processing (OLTP).      | Optimized for business intelligence, reporting, and dashboards. |

---

## 🔄 ETL Process (Extract, Transform, Load)

> **ETL** is the process that extracts data from various internal and external sources, transforms it using enterprise-wide definitions, and loads it into the data warehouse.

### ETL Workflow Components:

| Step      | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| Extract   | Pull data from multiple source systems such as POS, ERP, legacy OLTP, web documents, and external data. |
| Transform | Convert data into a common format and structure for consistency across the enterprise. |
| Load      | Insert transformed data into the data warehouse for analysis and reporting. |

- ETL supports **data integration** across many systems.
- The data warehouse framework includes metadata repositories, middleware, and data marts.

---

## 🗂️ Data Mart

> **Data Mart**: A subset of a data warehouse focused on a specific business unit or user group, containing summarized or highly focused data for targeted analysis.

- Enables **faster and more relevant decision support** for particular departments or functions.
- Often organized to provide reports, queries, and analytics such as data mining specific to that area.

---

## ⭐ Star Schema in Data Warehousing

- The **star schema** is a common data warehouse organization structure.

| Component        | Description                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------|
| Fact Table       | Large table storing measurable, quantitative data such as sales transactions. Usually "insert-only". |
| Dimension Tables | Smaller, generally static tables providing descriptive information about entities involved in facts (e.g., customers, products, stores). |

### Example Tables in Star Schema

| Fact Table (Orders)    | Dimension Tables                          |
|-----------------------|------------------------------------------|
| orderId, date, custId, prodId, storeId, qty, amt | Customers (custId, name, address, city), Products (prodId, name, price), Stores (storeId, city) |

- Fact tables contain **keys linking** to dimension tables.
- Dimension tables provide **contextual details** for facts.

---

## 💻 Structured Query Language (SQL) Example

- SQL is used to query data warehouses for analysis.

### Example Query

```sql
SELECT prodId, date, SUM(amt) AS amt
FROM SALE
GROUP BY prodId, date
```

- This query groups sales by product and date, summing amounts.
- SQL supports operations like **drill-down** (detailed view) and **rollup** (summary view).

---

## 🌐 Evolving Analytics Landscape

- The modern analytics environment includes diverse data sources:

| Data Type            | Description                            |
|----------------------|------------------------------------|
| Machine Data         | Data generated by machines/sensors. |
| Web Data             | Data from websites and online activity. |
| Audio/Video Data     | Multimedia data streams.              |
| External Data        | Third-party or external sources.     |
| Operational Systems  | Structured transaction data.         |
| Streaming/CEP Engine | Real-time complex event processing.  |
| Hadoop Cluster       | Distributed storage and processing for big data. |
| Analytical Platforms | Non-relational databases and BI servers. |

- Data flows through **ETL** processes (batch, near real-time, or real-time) into warehouses, sandboxes, and marts.
- Users range from **casual users** to **power users** utilizing in-memory BI sandboxes and analytical tools.

---

## ☁️ Examples of Data Warehouse Solutions

| Deployment Type | Example Solutions                                  |
|-----------------|---------------------------------------------------|
| On-premises     | Traditional enterprise data warehouses hosted locally. |
| Cloud           | Microsoft Fabric, Informatica Intelligent Data Management Cloud |

---

## 📊 Business Intelligence - Operational Value

> The **latency** between a business event and the action taken affects business value.

| Stage                | Description                             |
|----------------------|---------------------------------------|
| Data Latency         | Time from event occurrence to data availability for analysis. |
| Analysis Latency     | Time required to analyze data and generate insights.           |
| Decision Latency     | Time taken to make and execute decisions based on analysis.    |
| Action Time/Distance | Total time from event to action; shorter latency results in higher business value. |

---

# End of Lecture Content