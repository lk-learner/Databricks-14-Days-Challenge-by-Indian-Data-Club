# DAY 5 – Delta Lake Advanced 
## DataBricks 14-Day AI Challenge
---

<p align="center">
<img src="/Day 05/5_Badges.png" width=40% height=40%>

---
### 📌 Overview

Day 5 is about moving from "just storing data" to "governing and optimizing data." By the end of this module, you should be able to build resilient pipelines that handle changing schemas and perform efficiently at scale. Transition from basic table operations to advanced Delta Lake features that ensure performance, reliability, and data integrity in a production environment.

- Master the **MERGE** operation for Upserts.
- Understand **Schema Evolution** vs. **Schema Enforcement**.
- Implement **Time Travel** and **Table Restoration**.
- Optimize performance using **Z-Ordering** and **Compaction**.
- Maintain storage health with **VACUUM**.

---

### 📚 Learn:

- Time travel (version history)
- MERGE operations (upserts)
- OPTIMIZE & ZORDER
- VACUUM for cleanup

---

### 🛠️ Tasks:

1. Implement incremental MERGE
2. Query historical versions
3. Optimize tables
4. Clean old files
---

### 🔑 Key Concepts

**1. Advanced Data Manipulation (DML)**
MERGE Operation: This is the most critical concept. It allows you to perform "Upserts"—a combination of INSERT, UPDATE, and DELETE—in a single atomic transaction. This is essential for synchronizing streaming data or updating dimensions in a data warehouse.

**2. Schema Governance**
Schema Enforcement (Strictness): Delta Lake prevents "data pollution" by automatically rejecting any data that doesn't match the table's defined schema.

Schema Evolution (Flexibility): The ability to safely add new columns or change data types over time without rewriting the entire table, using the mergeSchema option.

**3. Data Reliability & History**
Time Travel: Accessing previous versions of your data using a version number or a specific timestamp. This is used for auditing, reproducing machine learning experiments, and accidental data recovery.

RESTORE Command: Quickly rolling back a table to a specific point in time if a pipeline error occurs.

**4. Performance Optimization**
File Compaction (OPTIMIZE): Consolidating many small Parquet files into fewer, larger files to reduce metadata overhead and speed up query processing.

Z-Ordering: A technique to co-locate related information in the same files. By Z-ordering on frequently filtered columns (like customer_id or date), you drastically reduce the amount of data Spark needs to read.

**5. Table Maintenance**
VACUUM: Permanently deleting data files that are no longer needed by the current version of the table (and are older than the retention period). This is vital for managing storage costs and meeting data privacy requirements like GDPR.

Transaction Log (_delta_log): Understanding how Delta Lake uses a JSON-based audit trail to provide ACID transactions and keep track of all changes.


---

### 💻 Hands-on Lab Practice:

```python
from delta.tables import DeltaTable

# MERGE for incremental updates
deltaTable = DeltaTable.forPath(spark, "/delta/events")
updates = spark.read.csv("/path/to/new_data.csv", header=True, inferSchema=True)

deltaTable.alias("t").merge(
    updates.alias("s"),
    "t.user_session = s.user_session AND t.event_time = s.event_time"
).whenMatchedUpdateAll() \
 .whenNotMatchedInsertAll() \
 .execute()

# Time travel
v0 = spark.read.format("delta").option("versionAsOf", 0).load("/delta/events")
yesterday = spark.read.format("delta") \
    .option("timestampAsOf", "2024-01-01").load("/delta/events")

# Optimize
spark.sql("OPTIMIZE events_table ZORDER BY (event_type, user_id)")
spark.sql("VACUUM events_table RETAIN 168 HOURS")

```

---

### 🔗 Resources:

- [Time Travel](https://www.databricks.com/blog/2019/02/04/introducing-delta-time-travel-for-large-scale-data-lakes.html)
- [MERGE Guide](https://docs.databricks.com/delta/merge.html)

