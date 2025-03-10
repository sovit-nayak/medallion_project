# 🏗️ Modern Data Engineering with Medallion Architecture using DBT, Databricks, Spark, and Azure Cloud

![Medallion Architecture][(https://github.com/sovit-nayak/medallion_project/blob/main/System_Architecture.jpeg)]
*Image Source: Wikipedia*

## 📌 Project Overview

This project demonstrates a **modern data engineering workflow** using **Azure Databricks, Apache Spark, and Data Build Tool (DBT)** with Azure as the cloud provider. It illustrates the **end-to-end process** of **data ingestion, transformation, and orchestration** using the **Medallion Architecture**.

### **🔹 Key Highlights**

- **Data Ingestion**: Storing raw data in **Azure Data Lake Storage (ADLS) Gen2**.
- **Data Processing & Integration**: Using **Azure Data Factory (ADF)** to manage pipelines.
- **Data Transformation**: Leveraging **Databricks** and **DBT** to refine data into **Bronze, Silver, and Gold layers**.
- **Security & Automation**: Managing secrets securely with **Azure Key Vault** and **Databricks Secret Scope**.
- **Data Marts & Documentation**: Using **DBT** for **snapshots, transformations, and documentation**.

---

## 📂 Table of Contents

1. [System Architecture](#-system-architecture)
2. [Prerequisites](#-prerequisites)
3. [Setup & Implementation](#-setup--implementation)
4. [Project Steps](#-project-steps)
5. [DBT Configuration](#-dbt-configuration)
6. [Results](#-results)
7. [Contributing](#-contributing)
8. [License](#-license)

---

## 🔧 System Architecture

This project follows the **Medallion Architecture** (Bronze, Silver, Gold) for data lakehouse implementation:

- **Bronze Layer**: Raw data ingestion
- **Silver Layer**: Data cleaning and transformation
- **Gold Layer**: Business-ready aggregated tables

---

## 🚀 Prerequisites

Before setting up, ensure you have:

- An **Azure Subscription**
- **Azure Storage Account** for **ADLS Gen2**
- **Azure Data Factory (ADF)**
- **Azure Databricks**
- **DBT (Data Build Tool) installed**
- **Python 3.x & Git installed**

---

## ⚙️ Setup & Implementation

### **Step 1: Azure Resource Setup**

1. **Creating Azure Resource Groups**
   Resource groups help manage and organize all the related services used in this project. A resource group is created to group the **storage account, Databricks workspace, Key Vault, and ADF instance** under a single manageable unit.
2. **Setting Up Azure Storage Account with Medallion Architecture**
   A **Data Lake Storage (ADLS) Gen2** account is set up to store raw data (Bronze), cleaned and structured data (Silver), and analytics-ready data (Gold). These layers follow the Medallion Architecture best practices.
3. **Configuring Azure Data Factory (ADF)**
   **ADF** is used to orchestrate and automate data movement. Linked services are created to connect Databricks, ADLS, Key Vault, and Azure SQL Database.
4. **Azure Key Vault Setup**
   Secrets and credentials (e.g., storage keys, database credentials, API tokens) are securely stored in **Azure Key Vault** to ensure **secure authentication and access control**.
5. **Creating an Azure SQL Database**
   A **metadata database** is set up in **Azure SQL** to store configurations and transformation logs for monitoring and auditing.

### **Step 2: Data Orchestration & Transformation**

6. **Building Azure Data Factory Pipelines**
   Pipelines are created in **ADF** to move data from source systems to ADLS. **Data movement, transformation, and scheduling** are automated using ADF’s data flow activities.
7. **Setting Up Azure Databricks**
   Databricks is provisioned to enable **big data processing and machine learning**. The Databricks environment is integrated with ADLS, ADF, and Key Vault for seamless data access.
8. **Configuring Databricks Secret Scope & Key Vault**
   Databricks **Secret Scope** is configured to fetch **secure credentials from Key Vault**, eliminating hardcoded credentials in Databricks notebooks.
9. **Verifying Databricks-Key Vault Integration**
   A test is conducted to validate whether **Databricks can securely retrieve secrets** (e.g., storage account keys, database passwords) from Key Vault.
10. **Integrating Azure Data Factory with Databricks**
    **ADF is integrated with Databricks** to trigger notebooks for data processing and transformation, ensuring an **automated ETL workflow**.

### **Step 3: DBT (Data Build Tool) Setup & Configuration**

11. **DBT Setup and Installation**
    DBT is installed and initialized to manage transformations and **create reusable data models**.
12. **Configuring DBT with Azure Databricks**
    The **profiles.yml** file is configured to establish **DBT-Databricks connectivity**, allowing transformation scripts to run within the Databricks environment.
13. **Running DBT Snapshots with ADLS Gen2**
    DBT **snapshots** are used to track **historical changes in data**, enabling **time-travel analysis and audit logs**.
14. **Creating DBT Data Marts**
    The **final Gold Layer data marts** are built using DBT models, optimizing data for business reporting and analytics.
15. **Generating DBT Documentation**
    DBT **automatically documents data models, dependencies, and transformations**, providing a **clear lineage of data movement**.

---

## 🏗️ DBT Configuration

To integrate **DBT** with **Databricks**, configure your `profiles.yml`:

```yaml
default:
  outputs:
    dev:
      type: databricks
      method: oauth
      schema: dbt_medallion
      host: adb-xxxx.azuredatabricks.net
      http_path: /sql/1.0/warehouses/xxx
      token: "{{ env_var('DATABRICKS_TOKEN') }}"
      threads: 4
  target: dev
```
