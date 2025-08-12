# DataVault-ECommerce-Project

### README.md

---

## Data Vault ELT Pipeline for E-Commerce Analytics 🛒

This project demonstrates the design and implementation of a scalable and auditable data pipeline using a Data Vault 2.0 methodology. The goal was to transform raw e-commerce data into a structured data warehouse and a business-ready reporting layer, showcasing skills in modern data engineering practices.

### 🎯 **Core Objective**

To build a robust and flexible Extract, Load, and Transform (ELT) pipeline that can handle a complex, multi-source dataset and deliver actionable insights for business reporting.

### 📦 **Data Source**

The project utilizes the **Brazilian E-Commerce Public Dataset by Olist** from Kaggle. This dataset is ideal for Data Vault modeling as it consists of multiple interconnected CSV files, including:
* Customers and their unique IDs
* Orders and their details
* Order items and payments
* Products and sellers

---

### 🗺️ **Project Architecture & Methodology**

The pipeline follows a layered architecture, a key principle of the Data Vault methodology.

1.  **Staging Layer**: Raw CSV files were ingested directly into a Microsoft Fabric Lakehouse. This layer serves as the landing zone for the untransformed data.
2.  **Raw Data Vault**: The core of the data warehouse. PySpark notebooks were used to create a Data Vault model consisting of three main table types:
    * **Hubs:** Representing core business entities (`Hub_Customer`, `Hub_Order`, `Hub_Product`, `Hub_Seller`).
    * **Links:** Modeling the relationships between these hubs (`Link_Customer_Order`, `Link_Order_Review`, `Link_OrderItem_Product_Seller`).
    * **Satellites:** Storing descriptive, historical attributes for each hub and link (`Sat_Customer_Details`, `Sat_Link_OrderItem_Product_Seller`, etc.).
3.  **Information Mart**: A denormalized table was created on top of the Data Vault to answer a specific business question: **"Who are the top 10 customers by total spending?"** This `Mart_Customer_Spending` table is optimized for quick reporting and analytics.

The use of **hash keys** for all hubs and links ensures that data loading can be performed in parallel, improving performance and scalability. 

---

### 🛠️ **Technologies Used**

* **Data Engineering**: Microsoft Fabric, PySpark, Jupyter Notebooks
* **Version Control**: Git / GitHub
* **Business Intelligence**: Power BI

---

### 📂 **Project Files**

* `staging_pipeline.ipynb`: PySpark code for ingesting raw CSVs and creating the staging tables in the Lakehouse.
* `hubs_creation.ipynb`: PySpark code to create all Hub tables (`Hub_Customer`, `Hub_Order`, etc.).
* `satellites_creation.ipynb`: PySpark code to create all Satellite tables.
* `links_creation.ipynb`: PySpark code to create all Link tables, including the resolution of the `customer_unique_id` join issue.
* `information_mart.ipynb`: PySpark code to create the final `Mart_Customer_Spending` table for reporting.
* `powerbi_dashboard.pdf`: A PDF of the final Power BI dashboard visualizing the top customers.

---
