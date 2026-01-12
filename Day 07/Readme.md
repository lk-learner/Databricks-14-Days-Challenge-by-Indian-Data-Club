# DAY 7 – Workflows & Job Orchestration
## DataBricks 14-Day AI Challenge

---
### 📌 Overview

Day 7 focuses on moving from manual execution to automated production. In this module, you learn how to use **Databricks Workflows** to string together various tasks—such as Notebooks, Python scripts, and Delta Live Tables—into a cohesive, automated pipeline. The goal is to ensure data processes run reliably, on schedule, or in response to specific events.

---

### 📚 Learn:

- Databricks Jobs vs notebooks
- Multi-task workflows
- Parameters & scheduling
- Error handling

---

### 🛠️ Tasks:

1. Add parameter widgets to notebooks
2. Create multi-task job (Bronze→Silver→Gold)
3. Set up dependencies
4. Schedule execution

---

### 🔑 Key Concepts

### 1. Databricks Jobs
A **Job** is the primary unit of orchestration in Databricks. It allows you to run a single task or a complex graph of dependent tasks.
* **Tasks:** The individual steps in a job (e.g., running a cleaning notebook, then a training script).
* **Job Clusters:** Dedicated, ephemeral compute resources that start when a job begins and terminate when it ends, significantly reducing costs.

### 2. Multi-Task Workflows (DAGs)
Workflows allow you to create **Directed Acyclic Graphs (DAGs)**. This means you can define dependencies where Task B only starts if Task A completes successfully. This is essential for ETL pipelines where transformation must follow ingestion.

### 3. Triggers & Scheduling
How do you start a workflow?
* **Scheduled:** Run daily, hourly, or via Cron expressions.
* **File Arrival:** Triggered automatically when new data lands in a cloud storage location (S3/ADLS).
* **Continuous:** Keeps the job running constantly for real-time processing.

### 4. Parameterization
Using **Widgets** and job parameters to pass values (like dates or file paths) into your notebooks dynamically at runtime. This allows the same workflow to be reused for different datasets.

### 5. Monitoring & Error Handling
* **Notifications:** Setting up Email or Slack alerts for job success, failure, or duration threshold breaches.
* **Retries:** Configuring automatic retries for tasks that might fail due to transient network issues.
* **Repair & Rerun:** The ability to fix a single failed task and resume the workflow from that point without restarting the entire job.

---

## 🚀 Practical Exercise
1. Create a job with at least two dependent tasks.
2. Configure a **Job Cluster** to optimize cost.
3. Set up a **Schedule** to run the job automatically.
4. Test a **Repair Run** by intentionally failing a task and then fixing it.

```python
# Add widgets for parameters
dbutils.widgets.text("source_path", "/default/path")
dbutils.widgets.dropdown("layer", "bronze", ["bronze","silver","gold"])

# Use parameters
source = dbutils.widgets.get("source_path")
layer = dbutils.widgets.get("layer")

def run_layer(layer_name):
    if layer_name == "bronze":
        # Bronze logic
        pass
    elif layer_name == "silver":
        # Silver logic
        pass
    # ...

# UI: Create Job
# Task 1: bronze_layer (notebook)
# Task 2: silver_layer (depends on Task 1)
# Task 3: gold_layer (depends on Task 2)
# Schedule: Daily 2 AM
```

---

### 🔗 Resources:

- [Jobs Documentation](https://docs.databricks.com/jobs/)
- [Job Parameters](https://docs.databricks.com/jobs/parameters.html)

---

@databricks @codebasics @indiandataclub #DatabricksWithIDC
