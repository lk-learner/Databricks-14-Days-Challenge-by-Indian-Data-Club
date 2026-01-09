# Day 2 – Apache Spark Fundamentals
## Databricks 14 Days AI Challenge

---

### 📌 Overview
Day 2 focuses on understanding the core engine behind Databricks: **Apache Spark**. We transition from high-level platform concepts to the architecture and APIs that enable distributed big data processing.

---

### 📚 Learn:

- Spark architecture (driver, executors, DAG)
- DataFrames vs RDDs
- Lazy evaluation
- Notebook magic commands (`%sql`, `%python`, `%fs`)
---
### 🛠️ Tasks:

1. Upload sample e-commerce CSV
2. Read data into DataFrame
3. Perform basic operations: select, filter, groupBy, orderBy
4. Export results

---

### 📖 Key Concepts
1. **Apache Spark Architecture**
   - **Driver Program:** The heart of the application; maintains state and schedules tasks.
   - **Worker Nodes:** Machines where the actual computation happens.
   - **Executors:** Processes on worker nodes that run the tasks.
   - **Cluster Manager:** Manages resources (e.g., Standalone, YARN, Kubernetes).

2. **Spark Components**
   - **Spark SQL:** For structured data processing.
   - **Spark Streaming:** For real-time data ingestion.
   - **MLlib:** Machine Learning library.
   - **GraphX:** For graph processing.

3. **Data Abstractions**
   - **RDD (Resilient Distributed Dataset):** The low-level foundation (Immutable & Fault-tolerant).
   - **DataFrames:** Distributed collections of data organized into named columns (the preferred API).
   - **Datasets:** Type-safe interface (primarily for Scala/Java).

---

### 🚀 Key Takeaways
- Spark uses Lazy Evaluation: Transformations are not executed until an Action (like count() or show()) is called.

- Databricks optimizes Spark workloads using the Photon engine for faster execution.
---

### 💻 Hands-on Lab: Spark Basics
In this session, we explore the Spark session and basic DataFrame operations:

```python
# Initialize Spark Session (Pre-configured in Databricks)
# Check the Spark version
print(f"Spark Version: {spark.version}")

# Load data
events = spark.read.csv("/path/to/sample.csv", header=True, inferSchema=True)

# Basic operations
events.select("event_type", "product_name", "price").show(10)
events.filter("price > 100").count()
events.groupBy("event_type").count().show()
top_brands = events.groupBy("brand").count().orderBy("count", ascending=False).limit(5)

```
---
### 🔗 Resources:

- [PySpark Guide](https://docs.databricks.com/pyspark/)
- [Spark SQL Guide](https://spark.apache.org/docs/latest/sql-programming-guide.html)

---
@databricks @codebasics @indiandataclub #DatabricksWithIDC
