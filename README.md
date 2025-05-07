# 🚦 **CrashDB: Comparative Study of SQL vs NoSQL for California Traffic Collision Analytics**

## 📌 **Project Overview:**
**CrashDB** is a comparative data engineering and analytics project analyzing **California traffic collision data (2019–2020)** using both **relational (MySQL)** and **NoSQL (MongoDB)** databases.

We explored how each database paradigm handles **large, complex, multi-entity traffic data**, and evaluated their strengths for storage, querying, normalization, and visualization in a real-world analytics pipeline.

Our goal was to answer:  
👉 *“Is a normalized relational schema or a flexible NoSQL document store better for traffic collision analysis?”*

---

## 🛠️ **Approach:**

✅ **Data Source:**
- 10GB dataset from **California Highway Patrol (via Kaggle)**
- Three main entities: **Collisions (9.4M rows), Parties (18.6M), Victims (9.6M)**

### 🏗️ **Relational Database (SQL - MySQL on AWS RDS):**
- Normalized dataset to **3rd Normal Form** (Snowflake schema)
- Created **9 relational tables**: Collisions, Parties, Victims, Vehicle Types, Weather Effects, Violations, etc.
- Implemented:
  - **Stored procedures** (e.g., Compare_Collisions_2019_2020)
  - **Triggers** for aggregating victims/parties per collision
- Connected MySQL **via Python (Jupyter)** for querying and analysis

### 🏢 **NoSQL Database (MongoDB Atlas):**
- Modeled data as **nested JSON documents** with embedded arrays
- Stored each collision record along with nested parties and victims data
- Designed **schema-less collections** allowing flexible data ingestion
- Queried data using **MongoDB aggregation pipelines**

---

## 📊 **Visualization & Analysis:**
- Both databases connected to **Tableau & Python visualization** workflows
- Created dashboards comparing:
  - Collisions by **time, location, weather, vehicle type**
  - Fatal vs non-fatal trends across **2019 vs 2020**
  - Alcohol influence, age groups, gender distributions
- Visual insights included:
  - **Highest collisions in Jan 2019, dropping during COVID lockdowns**
  - **Cloudy weather correlated with highest fatalities**
  - **13% collisions involved alcohol**
  - **Young adults (20-50) had highest fatality rate**

---

## 💡 **What We Learned:**

### ✅ **SQL Strengths:**
- Structured schema ensured **data integrity, referential constraints**
- Easier to perform **complex JOINs** across normalized tables
- Stored procedures & triggers helped automate **aggregated insights**

### ✅ **NoSQL Strengths:**
- **Faster data ingestion** due to schema flexibility
- Easier to query **nested, document-style data** for embedded parties/victims
- Scaled well for **read-heavy operations** without schema migration issues

---

## 🔍 **Key Comparative Findings:**

| Feature                      | Relational DB (SQL)      | NoSQL (MongoDB)        |
|-----------------------------|-------------------------|-----------------------|
| Schema Design                | Strict 3NF normalization | Flexible schema-less   |
| Data Integrity               | ✅ Strong (PK/FK)         | ❌ Application-managed |
| Querying Relationships       | ✅ SQL JOINs              | ❌ Requires nested queries |
| Ingestion Speed              | ❌ Slower                 | ✅ Faster              |
| Storage Efficiency           | ✅ Compact (normalized)   | ❌ Redundant (embedded) |
| Analytics Integration        | ✅ Tableau/Python         | ✅ Tableau/Python      |
| Aggregation Pipeline         | ✅ SQL GroupBy/Having     | ✅ Mongo Aggregations  |

---

## ✅ **What Went Well:**

🌟 Successfully normalized a **denormalized 10GB dataset into SQL snowflake schema**  
🌟 Modeled equivalent **nested JSON collections for NoSQL**  
🌟 Connected both databases to **Tableau & Python** for comparative visualization  
🌟 Built **stored procedures & aggregation pipelines** to standardize metrics

---

## ⚠️ **Challenges:**

😅 **Normalization vs denormalization trade-offs** → SQL required more joins, NoSQL had nested redundancy  
😅 **Maintaining referential integrity in NoSQL required extra coding at app level**  
😅 **Handling missing/ambiguous fields** (e.g., unknown gender) equally across both models  
😅 Query optimization for **large JOINs vs deep nested queries**

---

## 📝 **Conclusion: SQL vs NoSQL for California Traffic Collision Analysis**

### 🔍 **Performance:**
✅ **SQL performed better for complex queries involving multiple joins** across normalized tables.  
✅ **NoSQL had faster data ingestion and retrieval** for simple queries, especially when accessing embedded/nested documents.  
✅ For aggregation-heavy dashboards, **SQL’s stored procedures and GROUP BY queries showed more predictable performance**, while MongoDB aggregations scaled better for read-heavy workloads.

### 🏗️ **Complexity:**
✅ **SQL schema design was more complex upfront** due to 3rd Normal Form normalization and enforcing referential integrity.  
✅ **NoSQL schema design was simpler initially**, but required **application-level logic** to maintain data consistency (e.g., duplicated nested records).  
✅ Querying relationships (e.g., collisions → victims → parties) was **easier in SQL (via JOINs)** but required **nested queries in NoSQL** that were harder to write and optimize.

### 🏆 **Final Verdict:**

| Use Case                           | Recommended Database  |
|-----------------------------------|---------------------|
| Complex queries across multiple entities | ✅ **Relational (SQL)**  |
| Flexible schema, evolving data     | ✅ **NoSQL (MongoDB)**  |
| Data integrity & referential constraints | ✅ **Relational (SQL)**  |
| Fast ingestion of semi-structured data | ✅ **NoSQL (MongoDB)**  |
| Analytics on stable, structured dataset | ✅ **Relational (SQL)**  |
| Embedded/nested data analytics     | ✅ **NoSQL (MongoDB)**  |

👉 **For this project’s analytical goals (multi-entity joins, integrity, dashboard reporting), a relational database was the better fit.**  
👉 **However, NoSQL demonstrated clear advantages for rapid ingestion, flexible modeling, and handling nested relationships—ideal for scaling beyond structured schemas.**

✅ **Final takeaway: Use relational databases for structured, multi-relational analytics; leverage NoSQL for scalable, evolving, document-centric data pipelines.**
