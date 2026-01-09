# DAY 3: PySpark Transformations Deep Dive 🚀

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
