# DAY 3: PySpark Transformations Deep Dive

## DataBricks 14-Day AI Challenge

---
### 📌 Overview

On Day 3, we move beyond basic DataFrame operations to understand how Spark handles data under the hood. Mastering transformations is the key to writing efficient, scalable Spark jobs.

---

### 📚 Learn:

- PySpark vs Pandas comparison
- Joins (inner, left, right, outer)
- Window functions (running totals, rankings)
- User-Defined Functions (UDFs)

---

### 🛠️ Tasks:

1. Load full e-commerce dataset
2. Perform complex joins
3. Calculate running totals with window functions
4. Create derived features

---

### ⚡ 1. Transformations vs. Actions

Spark uses Lazy Evaluation. This means Spark doesn't execute the code immediately; it builds a DAG (Directed Acyclic Graph) and only runs when an Action is called.

| Feature | Transformations | Actions |
| :--- | :--- | :--- |
| **Definition** | Operations that create a new DataFrame from an existing one. | Operations that trigger computation and return a result. |
| **Examples** | `select()`, `filter()`, `groupBy()`, `join()` | `show()`, `collect()`, `count()`, `write()` |
| **Execution** | Lazy (Planning phase) | Eager (Execution phase) |


---

### 🔍 2. Narrow vs. Wide Transformations

Understanding the difference is critical for performance tuning.

**A. Narrow Transformations** 

- **Definition:** Each input partition contributes to only one output partition. No data movement across the network (No Shuffle).
- **Examples:** map(), filter(), union(), select().
- **Performance:** Very fast.

**B. Wide Transformations**

- **Definition:** Data from multiple input partitions is required to create a single output partition. Requires a Shuffle.
- **Examples:** groupBy(), join(), distinct(), orderBy().
- **Performance:** Expensive due to network I/O and disk spills.

---

### 💻 Hands-on Lab Practice:

```python
from pyspark.sql import functions as F
from pyspark.sql.window import Window

# Top 5 products by revenue
revenue = events.filter(F.col("event_type") == "purchase") \
    .groupBy("product_id", "product_name") \
    .agg(F.sum("price").alias("revenue")) \
    .orderBy(F.desc("revenue")).limit(5)

# Running total per user
window = Window.partitionBy("user_id").orderBy("event_time")
events.withColumn("cumulative_events", F.count("*").over(window))

# Conversion rate by category
events.groupBy("category_code", "event_type").count() \
    .pivot("event_type").sum("count") \
    .withColumn("conversion_rate", F.col("purchase")/F.col("view")*100)
```

---

### 🔗 Resources:

- [Window Functions](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/window.html)
- [PySpark Functions API](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/functions.html)
---
@databricks @codebasics @indiandataclub #DatabricksWithIDC
