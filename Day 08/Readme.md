
# DAY 8 – Unity Catalog Governance
## DataBricks 14-Day AI Challenge

---
### 📌 Overview

Day 8 is a shift from "building" to "managing." In a production AI environment, you cannot have "wild west" data access. Unity Catalog acts as the "brain" of the Databricks platform, ensuring that data scientists and engineers only see the data they are authorized to see. This day teaches you how to move away from the legacy Hive Metastore and embrace a unified governance layer that works across different cloud regions and workspaces.

---
### 📚 Learn:

- Catalog → Schema → Table hierarchy
- Access control (GRANT/REVOKE)
- Data lineage
- Managed vs external tables

---

### 🛠️ Tasks:

1. Create catalog & schemas
2. Register Delta tables
3. Set up permissions
4. Create views for controlled access


---

### 🔑 Key Concepts

**The Metastore:** The top-level container in Unity Catalog. It stores the metadata and permissions for all your data.

**Identity Federation:** The ability to use one set of users/groups across all your Databricks workspaces, ensuring consistent security.

**Three-Level Namespacing:** Unity Catalog uses a catalog.schema.table format, which provides an organized way to separate environments (e.g., prod.sales.orders vs dev.sales.orders).

**Volumes:** A newer concept in UC for governing non-tabular data (like PDFs, images, or CSVs) used in machine learning.

**Search and Discovery:** Leveraging the UI to find data quickly using keywords and tags, which is essential for large-scale AI projects.

---

### 📝 Practice:

```sql
-- Create structure
CREATE CATALOG ecommerce;
USE CATALOG ecommerce;
CREATE SCHEMA bronze;
CREATE SCHEMA silver;
CREATE SCHEMA gold;

-- Register tables
CREATE TABLE bronze.events USING DELTA LOCATION '/delta/bronze/events';
CREATE TABLE silver.events USING DELTA LOCATION '/delta/silver/events';
CREATE TABLE gold.products USING DELTA LOCATION '/delta/gold/products';

-- Permissions
GRANT SELECT ON TABLE gold.products TO `analysts@company.com`;
GRANT ALL PRIVILEGES ON SCHEMA silver TO `engineers@company.com`;

-- Controlled view
CREATE VIEW gold.top_products AS
SELECT product_name, revenue, conversion_rate
FROM gold.products
WHERE purchases > 10
ORDER BY revenue DESC LIMIT 100;

```
---
### 🔗 Resources:

- [Unity Catalog](https://docs.databricks.com/data-governance/unity-catalog/)
- [Getting Started](https://docs.databricks.com/data-governance/unity-catalog/get-started.html)

---
@databricks @codebasics @indiandataclub #DatabricksWithIDC
