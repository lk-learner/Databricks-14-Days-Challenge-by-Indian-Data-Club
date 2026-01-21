# DAY 10 – Performance Optimization
## DataBricks 14-Day AI Challenge

---

<p align="center">
<img src="Day 10/10-Days-Badge.png" width=40% height=40%>

---
### 📌 Overview

Day 10 focuses on the critical techniques required to make big data workloads faster and more cost-efficient within the Databricks environment. While Spark is powerful out of the box, handling petabyte-scale data requires specific strategies like Data Skipping, Z-Ordering, and Caching to reduce resource consumption and minimize query latency. This day bridges the gap between functional data engineering and high-performance data architecture.

---
### Learn:

- Query execution plans
- Partitioning strategies
- OPTIMIZE & ZORDER
- Caching techniques

---
### 🛠️ Tasks:

1. Analyze query plans
2. Partition large tables
3. Apply ZORDER
4. Benchmark improvements

---

### 🔑 Key Concepts

**Z-Ordering (Multi-dimensional Clustering):** A technique to colocate related information in the same set of files. This significantly enhances the effectiveness of data skipping.

**Data Skipping:** Delta Lake automatically collects statistics (min/max values) for the first 32 columns. Spark uses these to skip reading files that don't contain relevant data.

**Optimize Command:** The process of compacting small files into larger, more efficient files (target size ~1GB) to solve the "small file problem."

**Caching Strategies:** Disk Cache (Delta Cache): Stores copies of remote data on local NVMe SSDs for rapid subsequent reads.

**Spark Cache:** Storing DataFrames in memory (.persist()) for iterative algorithms.

**Adaptive Query Execution (AQE):** A Spark 3.x feature that re-optimizes query plans during runtime based on actual data statistics (e.g., handling data skew or coalescing partitions).


---
### 📝 Hands on Lab Practice:

```python
# Explain query
spark.sql("SELECT * FROM silver.events WHERE event_type='purchase'").explain(True)

# Partitioned table
spark.sql("""
  CREATE TABLE silver.events_part
  USING DELTA
  PARTITIONED BY (event_date, event_type)
  AS SELECT * FROM silver.events
""")

# Optimize
spark.sql("OPTIMIZE silver.events_part ZORDER BY (user_id, product_id)")

# Benchmark
import time
start = time.time()
spark.sql("SELECT * FROM silver.events WHERE user_id=12345").count()
print(f"Time: {time.time()-start:.2f}s")

# Cache for iterative queries
cached = spark.table("silver.events").cache()
cached.count()  # Materialize

```
---
### 🔗 Resources:

- [Performance Tuning](https://docs.databricks.com/performance/)
- [Optimization Guide](https://docs.databricks.com/delta/optimizations-oss.html)
---
@databricks @codebasics @indiandataclub #DatabricksWithIDC
