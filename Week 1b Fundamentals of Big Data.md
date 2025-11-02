## 🔍 Fundamentals of Big Data

### Introduction to Big Data Analytics

- **Big Data Analytics** involves analyzing large, diverse sets of data from various sources to uncover hidden patterns, correlations, and insights.
- Key components discussed include:
  - **Sources** of big data
  - **Characteristics** of big data
  - **Applications** across industries

---

## 📚 Course Structure and Key Topics

| Week | Date       | Topics Covered                                                                                              |
|-------|------------|------------------------------------------------------------------------------------------------------------|
| 1     | Sep. 08    | Fundamentals of Big Data – evolution, characteristics, applications, examples                              |
| 2     | Sep. 15    | Review of RDBMS concepts; Differences between OLAP and OLTP; Data warehouses, ETL/ELT, star schemas        |
| 3     | Sep. 22    | Big Data Management with NoSQL Databases; MongoDB lab                                                      |
| 4     | Sep. 29    | Continued NoSQL Databases; Cassandra lab                                                                   |
| 5     | Oct. 06    | Batch Processing of Big Data – HDFS, Map-Reduce, Hadoop Ecosystem                                          |
| 6     | Oct. 13    | Reading week                                                                                               |
| 7     | Oct. 20    | Big Data In-memory Processing – Apache Spark core architecture, APIs, Spark ecosystem                      |
| 8     | Oct. 27    | Managing Data Processing Clusters and Pipelines – Databricks Community Edition                             |
| 9     | Nov. 03    | Midterm Exam                                                                                               |
| 10    | Nov. 10    | Databricks with RDDs, DataSets, SparkSQL, pipelines                                                        |
| 11    | Nov. 17    | Advanced Analytics with Spark – Streaming, ML introduction                                                 |
| 12    | Nov. 24    | Azure Big Data Landscape – Microsoft cloud services                                                       |
| 13    | Dec. 01    | Cloud Infrastructure – MS Azure, HDInsight, stream analytics                                               |
| TBD   | TBD        | Final Exam (Brightspace, take-home)                                                                        |

---

## 📅 Course Deliverables and Grading

| Deliverable              | Due Date          | Weight on Final Grade |
|-------------------------|-------------------|----------------------|
| Weekly Quizzes          | Weeks 2,3,4,5,6,8,9,10,11,12 | Not specified        |
| Assignment 1            | Sep. 15 – Sep. 29 | 10%                  |
| Assignment 2            | Oct. 27 – Nov. 24 | 15%                  |
| Assignment 3            | Nov. 24 – Dec. 15 | 15%                  |
| Course Project          | Nov. 24 – Dec. 15 | 10%                  |
| Midterm Exam            | Nov. 03           | 10%                  |
| Final Exam (Multiple Choice + Take-home) | TBD               | 40% (range 25%-40%)  |

---

## 📚 Recommended Course Texts

| Author(s)                | Title                                                        | Publisher & Year           |
|-------------------------|--------------------------------------------------------------|----------------------------|
| Nuckolls, R. L.          | *Azure Storage, Streaming, and Batch Analytics*              | Manning Publications, 2020 |
| Chambers, B. & Zaharia, M. | *Spark: The Definitive Guide*                                | O’Reilly Media, 2018       |
| Perrin, J.               | *Spark in Action*                                             | Manning Publications, 2020 |
| Linoff, G. & Berry, M.   | *Data Mining Techniques for Marketing, Sales, and CRM*       | Wiley, 2011                |
| Han, J., Kamber, M., Pei, J. | *Data Mining: Concepts and Techniques*                      | Morgan Kaufmann, 2011      |
| Olson, D. & Shi, Y.      | *Introduction to Business Data Mining*                        | McGraw-Hill Irwin, 2007    |
| Dunham, M. H.            | *Data Mining, Introductory and Advanced Topics*               | Prentice Hall, 2003        |

---

## 🏢 Traditional Analytics vs. Big Data

| Aspect                  | Traditional Analytics                                | Big Data Analytics (Implied)                          |
|-------------------------|-----------------------------------------------------|------------------------------------------------------|
| Data Type               | Mostly **structured** data with known schema        | Includes structured, semi-structured, and unstructured data |
| Data Storage            | Data marts and data warehouses                        | Distributed storage systems like Hadoop, NoSQL       |
| Analytics Outputs       | Reports and dashboards                                | Real-time analytics, predictive models, and more complex insights |
| Infrastructure Ownership| Owned by the business                                 | Often involves cloud/commercial platforms             |

> **Traditional analytics** depends on well-structured databases and predefined data models, limiting scope and agility.

---

## 🌊 The Data Flood: Sources and Scale of Big Data

### Industries Generating Large Data Volumes

- Retail
- Banking and financial transactions
- Telecom and mobile phone services
- Web clickstreams
- Social media platforms
- E-commerce
- Healthcare
- Scientific research (astronomy, biology)

### Global Data Market

- The **big data technology and services market** was valued at over **$50 billion in 2020**.
- Data continues to grow exponentially, with **over 90% of data generated within the last 12 months**.

---

## 🌐 Data Sources Across Industries

| Industry                  | Data Source Examples                            |
|---------------------------|------------------------------------------------|
| Automotive                | Auto sensors reporting location and problems   |
| High Tech / Industrial Mfg | Manufacturing quality and warranty analysis    |
| Oil \& Gas                | Drilling and exploration sensor data            |
| Communications            | Location-based advertising                       |
| Life Sciences             | Clinical trials, genomics                        |
| Retail                    | Consumer sentiment, optimized marketing         |
| Consumer Packaged Goods   | Sentiment analysis, customer service             |
| Media / Entertainment     | Viewer data, advertising effectiveness           |
| Travel \& Transportation   | Traffic flow sensors, customer sentiment          |
| Financial Services        | Risk and portfolio analysis, product innovation  |
| Online Services / Social Media | Website optimization, people matching        |
| Utilities                 | Smart meter analysis for network capacity         |
| Education \& Research      | Experiment sensor analysis                          |
| Healthcare                | Patient sensors, electronic health records (EHR), quality of care |
| Law Enforcement \& Defense | Threat analysis, social media monitoring, photo analysis |

---

## 🧩 Data Structures: Types and Definitions

| Data Type        | Description                                                                                 | Examples                                    |
|------------------|---------------------------------------------------------------------------------------------|---------------------------------------------|
| **Structured**   | Data with a predefined schema before database creation; limited scope; relational databases | Relational databases, spreadsheets          |
| **Unstructured** | No predefined schema; large quantities of data such as video, voice, social media content   | Video, voice recordings, social media posts |
| **Semi-structured** | Data with some organizational properties but no strict schema                             | XML, JSON, YAML documents                    |

---

## 📊 Data Spectrum: From Structured to Unstructured

| **Structured Data**            | **Semi-Structured Data**         | **Unstructured Data**                        |
|-------------------------------|---------------------------------|---------------------------------------------|
| Relational databases           | XML documents                   | Web logs, web pages                          |
| Spreadsheets                  | RSS feeds                      | Emails, word processing files                |
| Flat files in record format    | EDI documents                  | Multimedia content (videos, streaming)      |
| Multi-dimensional databases    | JSON                          | Instant messaging, voice recognition         |
|                               | Taxonomies, ontologies        | Cloud storage, document management           |
|                               | Wikis                         |                                             |

---

## 🔢 Types of Data Generation

| Data Type       | Description                                | Examples                                   |
|-----------------|--------------------------------------------|--------------------------------------------|
| Transactional   | Data from trade and financial services    | Sales records, bank transactions            |
| Non-Transactional | Machine-generated event data               | IoT sensor outputs                           |
| Sub-Transactional | Events from telecom and social media        | Call records, social media activity logs    |

---

## 📈 Data Growth Insights

- More than **80% of data** generated is **unstructured**.
- The **annual size of the global datasphere** is rapidly increasing, reaching approximately **175 zettabytes**.
- Over **90% of the data known today** was generated in just the past **12 months**.

---

## ⚠️ Limitations of Traditional Analytics Approaches

- **Data integration complexity**: Organizational data often resides in isolated silos.
- Traditional analytics struggles to handle the volume, velocity, and variety of modern big data.
- Legacy systems are not designed for rapidly changing and diverse data forms.

---

# End of Week 1 Content

## ⚠️ Challenges in Traditional Data Analytics

- **Complexity and Cost**: Traditional data analysis methods are complex, time-consuming, and expensive.
- **Skills Scarcity**: Modern data requires new skills and methodologies for analysis, especially for cloud data.
- **Lack of Real-Time Analytics**: Conventional analytics mostly rely on historical data (batch processing) and do not support streaming or real-time data.
- **Data-to-Insight Gap**: Slow integration of data causes delays in obtaining actionable insights, sometimes taking days or weeks.

---

## 📊 Big Data: Definitions and Characteristics

### Definitions from Various Sources

| Source                         | Definition                                                                                              |
|--------------------------------|-----------------------------------------------------------------------------------------------------|
| **Gartner (2012)**             | Big Data are high-volume, high-velocity, and/or high-variety information assets requiring new processing forms to enable enhanced decision making, insight discovery, and process optimization. |
| **Wikipedia**                  | Big Data refers to data sets so large and complex they are difficult to process using traditional database tools. Challenges include capture, creation, storage, search, sharing, analysis, and visualization. |
| **IBM Big Data Platform**      | Big Data realizes greater business intelligence by storing, processing, and analyzing data previously ignored due to traditional technology limitations. |

---

## 📈 Important Big Data Market Trends and Growth

| Industry                        | Market Size (2021)          | CAGR (Compound Annual Growth Rate)       | Expected Market Size (Future)      |
|--------------------------------|-----------------------------|------------------------------------------|-----------------------------------|
| Healthcare                     | $20.12 billion              | 28.9% (2022-2028)                        | $79.23 billion (2028)             |
| Supply Chain Analytics         | $5.8 billion                | 17.93% (2021-2027)                       | $15.6 billion (2027)              |
| Banking Industry               | $4.93 billion               | 19.4% (2022-2031)                        | $28.11 billion (2031)             |
| Software                      | $162.6 billion              | 11.4% (2022-2027)                        | Not specified                    |

> **CAGR**: Rate of return assuming all profits are reinvested annually.

---

## 🌐 How Big is Big Data?

- Big Data challenges current technology in terms of:
  - **Volume**: Large amounts of data.
  - **Speed**: Fast data generation and processing.
  - **Analysis Power**: Ability to analyze complex data.
- **Note**: What qualifies as "big" data today may not be considered big tomorrow due to technological advances.

---

## 🔍 The 5Vs of Big Data

| V          | Explanation                                                                                  | Examples / Details                                                  |
|------------|----------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| **Volume** | Large amounts of data.                                                                        | 1 page ≈ 4 KB; 1 GB ≈ 560,000 pages; 1 PB ≈ 11,000 4K movies.    |
| **Variety**| Different types of data structures.                                                         | Structured (tables), semi-structured (XML, JSON), unstructured (images, videos, emails). |
| **Velocity**| Speed at which data is generated and processed.                                            | Batch, real-time, streaming (IoT devices).                         |
| **Veracity**| Trustworthiness and quality of data, including anomalies and noise.                         | Measures schema conformity, accuracy, accountability.             |
| **Value**  | Business insights gained from data analytics.                                               | More analysis leads to more valuable insights.                     |

---

## 📊 What Can Be Done With Big Data?

| Activity             | Description / Tools                                                              |
|----------------------|---------------------------------------------------------------------------------|
| **Aggregation & Reports** | OLAP, Visualization                                                          |
| **Searching & Querying**  | Keyword search, semantic search, pattern matching                             |
| **Knowledge Discovery**   | Data analytics, data mining, artificial intelligence (AI)                     |
| **Database Management**   | Relational databases (RDBS), NoSQL                                           |
| **Data Analytics Software** | Hadoop, Apache Spark, Cloud data warehouses                                |
| **Data Visualization**    | Tableau, Power BI                                                             |

---

## ☁️ Cloud Analytics: Intersection of Cloud Computing and Big Data

### Definitions

| Source    | Definition                                                                                          |
|-----------|--------------------------------------------------------------------------------------------------|
| **TIBCO** | Service and delivery model for business data analysis and computation using cloud technologies.   |
| **Splunk**| Process of storing and analyzing data in the cloud to extract actionable business insights.      |

### Cloud Analytics Process

| Step    | Description                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| **Ingest** | Data sources include cloud services, applications, databases, IoT devices producing JSON, XML, logs, configs. |
| **Process**| Complex processing of big data not suitable for traditional tools.                                           |
| **Analyze**| Challenge of analyzing very large and complex datasets to gain business insights.                            |

---

## ☁️ Cloud Deployment Models & Cloud Analytics

| Cloud Model   | Description                                                                                  | Usage Example                                  |
|---------------|----------------------------------------------------------------------------------------------|------------------------------------------------|
| **Private Cloud** | Owned by a single organization; provides privacy and data security.                         | Sensitive data storage and processing          |
| **Hybrid Cloud**  | Combines private and public clouds; sensitive data in private cloud, non-sensitive in public. | Balanced security and flexibility               |
| **Public Cloud**  | Offers publicly available services with metered usage.                                   | Data analytics on cloud services data           |

**Example Providers**: Google, Amazon, Microsoft, Salesforce, Yahoo, Zoho, Rackspace

---

## ☁️ Cloud Analytics: New Picture

- Data comes from various sources and cloud services.
- Data structures may be unknown and rapidly changing.
- No fixed models for much of the data.
- Analytics systems handle more data than traditional warehouses.
- Results are delivered as reports and dashboards.

---

## ⚙️ Components of Cloud Analytics

| Component           | Function                                                                                     |
|---------------------|----------------------------------------------------------------------------------------------|
| **Data Sources**    | Supports "big" data inputs from varied origins.                                             |
| **Data Models**     | Structures to retrieve and standardize relationships between data points; extraction is complex. |
| **Computing Power** | Sufficient resources needed for data extraction and processing.                             |
| **Processing Apps** | Specialized software to handle large volumes stored in cloud storage/data lakes.            |
| **Analytics Models**| Mathematical models including AI and Machine Learning (ML) for analysis and prediction.     |
| **Data Sharing & Storage** | Approaches to store both structured and unstructured data to support multiple applications and visualization tools. |

---

## 💡 Benefits of Cloud Analytics

| Benefit           | Explanation                                                                                     |
|-------------------|------------------------------------------------------------------------------------------------|
| **Cost Reduction** | Avoids expensive data centers; benefits from cloud scalability and service models.             |
| **Data Consolidation** | Efficiently processes data from websites, social media, cloud servers, etc., for insights.  |
| **Scalability**   | Can scale analytics on demand to handle growing data volumes.                                   |
| **Security**      | Improved data protection especially in private and hybrid clouds.                               |
| **Sharing & Collaboration** | Easier sharing of insights and collaboration across teams and organizations.              |

---

## ☁️ Cloud Analytics vs. Big Data Analytics

| Aspect              | Cloud Analytics                                               | Big Data Analytics                                      |
|---------------------|---------------------------------------------------------------|---------------------------------------------------------|
| **Focus**           | Building cloud infrastructure and services for analytics.      | Processing and analyzing large data sets, often cloud-hosted. |
| **Characteristics** | Uses cloud computing advantages: cost, scalability, efficiency. | Deals with big data specifically, which may or may not be cloud-based. |
| **Relationship**    | Cloud Analytics supports and enables Big Data Analytics.       | Big Data Analytics relies heavily on cloud infrastructure. |

---

## 🏭 Industry Applications of Big Data Analytics

- Manufacturing
- Retail
- Healthcare
- Oil and Gas
- Telecommunications
- Financial Services

---

## 🏥 Healthcare Big Data Challenges and Market Growth

- **Healthcare Data Growth**: Digital healthcare data grew from 500 PB in 2012 to 25,000 PB in 2020.
- **Market Size**: Valued at approximately $20.13 billion in 2021.
- **Growth Forecast**: Expected to reach around $79.3 billion by 2028.
- **CAGR**: Approximately 28.11% growth rate.

---

# End of Lecture Content

## 📊 Big Data Analytics in Healthcare

### **Patient Data Volume and Characteristics**
- A typical large hospital manages up to **665 TB of patient data**.
- **80% of patient data are unstructured medical image data** such as CT scans, MRI, and X-rays.
- Medical image data is **huge, high-dimensional, and complex**, requiring computationally intensive methods for extracting useful information.
- Medical archives grow annually by **20-40%**, increasing storage and analysis challenges.

### **Goals of Big Data Analytics in Healthcare**
| Goal                         | Description                                                    |
|------------------------------|----------------------------------------------------------------|
| Improved Quality of Care      | Reduce wait times, hospitalization length, and healthcare costs. |
| Timely Intervention          | Provide the right intervention at the right time.              |
| Process Streamlining          | Reduce operational costs by optimizing healthcare processes.   |
| Smarter Decisions            | Use data-driven decisions to improve patient outcomes.         |
| Early Disease Detection       | Detect disease outbreaks early for quicker response.           |
| Social Behavior Discovery     | Discover new social behaviors impacting health.                |

### **Types of Data in Healthcare**
- **Electronic Health Records (EHR)**
- **Genomic Data**
- **Sensor Data**
- **Public Health Data**
- **Behavioral Data**

---

## 🧠 The BRAIN Initiative

- A US NIH project aiming to **advance understanding of the human brain** and **accelerate new neurological treatments**.
- Brain activity data such as **EEG (Electroencephalography)** produce **high-volume, high-velocity data**.
- Example: A five-day epilepsy evaluation generates **about 1.6 GB of EEG data per patient**.
- EEG is analogous to ECG, but for brain activity (similar to how ECG measures heart activity).

---

## 🧬 Human Genome Analytics on MS Azure

- Virginia Tech leads with a **$550 million portfolio** in DNA sequencing projects.
- Produces over **15 PB of genome data annually**, initially struggling to analyze data fast enough.
- Adopted a **cloud computing model** using Microsoft Azure HDInsight:
  - Genome analysis time reduced from **2 weeks per genome to over 100 genomes per day**.
  - Cost dropped from **$100 million per genome in 2001 to under $6,000 per genome by 2016**.
- Veritas Genetics (as of Sept 2022) offers whole genome sequencing for **$599 via a smartphone app**.

---

## 📡 IoT and Body Area Sensor Networks (BASN)

- **Mobile computing and smartphones** create new healthcare opportunities.
- BASNs support **real-time decision-making and treatment**.
- Sensors monitor vital signs and internal functions:
  - Breathing activity
  - ECG and heart rate
  - Insulin pumps
  - Blood pH, glucose levels, temperature
  - Dissolved oxygen and carbon dioxide levels
- Useful for **Chronic and Acute Care patients** by continuously measuring physiological data.

---

## 🏭 Big Data in Manufacturing

| Application               | Description                                                                                     | Challenges                                                      |
|---------------------------|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| Predictive Maintenance     | Predict equipment failure using structured (age, make, model) and unstructured data (logs, sensors). | Integrating data from various devices/vendors.                  |
| Operational Efficiency     | Analyze production processes to better respond to customer feedback and demand-supply fluctuations. | Speedy analysis to identify failure signals.                    |
| Production Optimization     | Identify bottlenecks and delays in production lines.                                            | Balancing growing data volume with multiple users and sources.  |

---

## 🛍️ Big Data in Retail

| Focus Area              | Description                                                                                      | Challenges                                                     |
|-------------------------|--------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Product Development      | Anticipate demand, analyze focus group and social media data, model product attributes.          | Customer segmentation requires complex high-volume data analysis. |
| Customer Experience     | Fine-tune operations using social media, web visits, and call logs data.                         | Integrating diverse data sources is complex and challenging.   |
| Customer Lifetime Value | Analyze spending patterns, preferences, loyalty; reduce churn through proactive management.      | High-volume transaction data analysis is complex and resource-intensive. |

---

## 🛢️ Big Data in Oil & Gas

| Application              | Description                                                                                     | Challenges                                                      |
|--------------------------|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| Oil Exploration          | Analyze seismic data to find overlooked traces; inform decisions on new drilling sites.          | Integration of huge volumes of unstructured data.               |
| Predictive Maintenance   | Monitor remote offshore equipment to predict remaining life and optimize production efficiency. | Various data formats complicate quick operational analysis.     |
| Production Optimization  | Compare sensor data to predictions to understand discrepancies in well outputs.                  | Accuracy critical as errors can be very expensive.              |

---

## 💳 Big Data in Financial Services

| Application              | Description                                                                                     | Challenges                                                      |
|--------------------------|-------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| Fraud and Compliance      | Identify fraud patterns; aggregate data for regulatory reporting.                               | Integrating transaction and behavioral data at scale.          |
| Drive Innovation         | Use insights to innovate products, understand market trends, and improve decision-making.       | Need to build advanced risk models quickly on large datasets.   |
| Anti-money Laundering    | Detect fraud patterns to comply with government regulations.                                    | Managing large-scale data integration and analysis.             |

---

## 📈 Big Data Analytics Data Processing Pyramid

| Level              | Description                              | Tools and Technologies                                 |
|--------------------|------------------------------------------|-------------------------------------------------------|
| Big Data           | Raw data collected from various sources  | Hadoop (HDFS, MapReduce), NoSQL databases (HBase, Cassandra, MongoDB) |
| Information        | Extracted and structured data             | Data Warehouses, Hive, Pig, Data Lakes                 |
| Actionable Insights| Insights derived for decision-making     | Visualization (Reports, Dashboards), Data Mining, MLlib, GraphX, Azure Stream Analytics |

**Popular Big Data Tools**

| Category           | Tools                                      |
|--------------------|--------------------------------------------|
| Cluster Management | Yarn, Zookeeper                            |
| File System        | HDFS, Data Lake                            |
| Stream Processing  | Storm, Kafka                              |
| Batch Processing   | Hadoop, Spark                            |
| Data Analytics     | MapReduce, Spark                         |
| AI & ML            | Mahout, MLlib                           |
| Workflow           | Python, Scala, USQL, Data Factory        |

---

## ⚠️ Challenges to Big Data Analytics

| Challenge          | Description                                                      |
|--------------------|------------------------------------------------------------------|
| Data Governance    | Data must be stored across multiple global data centers.        |
| Data Capture      | Ensuring datasets are accurate, consistent, and relevant is complex and error-prone. |
| Data Cleansing    | Cleaning data to maintain quality before analysis is difficult.  |
| Storage          | Cloud offers advantages but on-premises silos pose challenges.   |
| Security         | Healthcare data security can limit cloud analytics capabilities. |
| Querying Data    | Data variety and format differences require time-consuming transformations. |

---

## 📚 References

- [What is Cloud Analytics?](https://www.tibco.com/reference-center/what-is-cloud-analytics)
- [Brain Initiative](https://www.whitehouse.gov/share/brain-initiative)
- [Virginia Tech Customer Story](https://www.microsoft.com/en/server-cloud/cloud-os/customer-stories/virginia-tech.aspx)
- [Limitations of Traditional Analytics](https://www.mycustomer.com/experience/engagement/understanding-customer-journeys-the-four-limitations-of-traditional-analytics)
- [Challenges with Big Data Analytics in Healthcare](https://healthitanalytics.com/news/top-10-challenges-of-big-data-analytics-in-healthcare)
- [Big Data Analytics Market Overview](https://cloudtweaks.com/2016/06/big-data-analytics-50-billion-dollar-market-2019/)
- [Global Big Data Analytics in Healthcare](https://onlinebeststor.com/global-big-data-analytics-in-healthcare-market-set-for-rapid-growth-to-reach-around-usd-68-03-billion-by-2024/)
- [Top Big Data Analytics Use Cases](https://www.oracle.com/a/ocom/docs/top-22-use-cases-for-big-data.pdf)