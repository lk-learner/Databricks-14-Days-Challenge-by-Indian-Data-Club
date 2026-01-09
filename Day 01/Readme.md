# Databricks 14-Day AI Challenge

## Day 1: Platform Setup & First Steps

### 🚀 Overview
Day 1 is focused on setting up your environment and understanding the foundational components of the Databricks Data Intelligence Platform. The goal is to move from a traditional developer or analyst mindset into the world of Lakehouse architecture.

### 📚 Learn:
- Why Databricks vs Pandas/Hadoop?
- Lakehouse architecture basics
- Databricks workspace structure
- Industry use cases (Netflix, Shell, Comcast)

### 🛠️ Tasks:
- **Account Setup**: Sign up for the [Databricks Community Edition](https://community.cloud.databricks.com/login.html) 
- **Workspace Exploration**: Familiarize yourself with the Databricks UI, including the Workspace, Catalog, and Compute sections.
- **Compute Configuration**: Create your first Spark Cluster (Personal Compute) to run notebooks.
- **Data Ingestion Basics**: Learn how to upload a CSV/JSON file to the Databricks File System (DBFS).
- **Notebook Fundamentals**: Create your first notebook and run basic SQL/Python commands.

### 📚 Key Concepts
- **Lakehouse Architecture**: Understanding how Databricks combines the performance of a data warehouse with the flexibility of a data lake.
- **Unity Catalog**: Introduction to fine-grained governance for data and AI assets.
- **Compute vs. Storage**: How Databricks separates compute resources from data storage.

### 💻 First Code Snippet (Python)
```python
# Check Databricks Runtime version
spark.version

# Create simple DataFrame
data = [("iPhone", 999), ("Samsung", 799), ("MacBook", 1299)]
df = spark.createDataFrame(data, ["product", "price"])
df.show()

# Filter expensive products
df.filter(df.price > 1000).show()

```

@databricks @codebasics @indiandataclub #DatabricksWithIDC

