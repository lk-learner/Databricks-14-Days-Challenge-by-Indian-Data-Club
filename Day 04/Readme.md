# DAY 4 – Delta Lake Introduction
## DataBricks 14-Day AI Challenge

---
### 🌟 Overview

Delta Lake is an open-source storage layer that brings ACID (Atomicity, Consistency, Isolation, Durability) transactions to Apache Spark and big data workloads. It provides a reliable way to manage a "Lakehouse" architecture by combining the best features of data warehouses and data lakes.

---
### 📚 Learn:

- What is Delta Lake?
- ACID transactions
- Schema enforcement
- Delta vs Parquet

### 🛠️ Tasks:

1. Convert CSV to Delta format
2. Create Delta tables (SQL and PySpark)
3. Test schema enforcement
4. Handle duplicate inserts

---

### 🔑 Key Concepts

- **ACID Transactions:** Ensures data integrity by preventing partial writes and failed job corruption.

- **Schema Enforcement:** Prevents "data swamps" by ensuring data being written matches the table's defined schema.

- **Time Travel:** Allows you to query previous versions of your data for auditing or rollbacks.

- **Unified Batch/Streaming:** A single table can act as both a batch source and a streaming sink.

---

### 💻 Hands-on Lab Practice:
```python
# Convert to Delta
events.write.format("delta").mode("overwrite").save("/delta/events")

# Create managed table
events.write.format("delta").saveAsTable("events_table")

# SQL approach
spark.sql("""
    CREATE TABLE events_delta
    USING DELTA
    AS SELECT * FROM events_table
""")

# Test schema enforcement
try:
    wrong_schema = spark.createDataFrame([("a","b","c")], ["x","y","z"])
    wrong_schema.write.format("delta").mode("append").save("/delta/events")
except Exception as e:
    print(f"Schema enforcement: {e}")

```

