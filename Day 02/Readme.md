# Day 2 – Apache Spark Fundamentals
## Databricks 14 Days AI Challenge

---

### 🚀 Key Takeaways
- Spark uses Lazy Evaluation: Transformations are not executed until an Action (like count() or show()) is called.

- Databricks optimizes Spark workloads using the Photon engine for faster execution.

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

### 📌 Overview
Day 2 focuses on understanding the core engine behind Databricks: **Apache Spark**. We transition from high-level platform concepts to the architecture and APIs that enable distributed big data processing.

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

### 💻 Hands-on Lab: Spark Basics
In this session, we explore the Spark session and basic DataFrame operations:

```python
# Initialize Spark Session (Pre-configured in Databricks)
# Check the Spark version
print(f"Spark Version: {spark.version}")

# Create a simple DataFrame
data = [("Alice", 34), ("Bob", 45), ("Catherine", 29)]
columns = ["Name", "Age"]
df = spark.createDataFrame(data, columns)

# Display the data
display(df)

# Basic Transformation: Filter
filtered_df = df.filter(df.Age > 30)
display(filtered_df)

