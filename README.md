# 🧾 Sales ETL Data Engineering Project (TEAM IICS TITANS - Informatica IICS)

## 📌 Overview

This project demonstrates an end-to-end **ETL (Extract, Transform, Load)** pipeline built using **Informatica Intelligent Cloud Services (IICS)**.

The goal is to:

* Clean dirty transactional data
* Validate and standardize records
* Enrich data using master datasets
* Generate analytical reports for business insights

---

## 📂 Dataset Description

The project uses the following CSV files:

* `sales_transactions.csv` → Clean transactional data
* `sales_transactions_dirty.csv` → Dirty data requiring cleansing
* `product_master.csv` → Product details (price, category, brand)
* `store_master.csv` → Store details (location, name)

---

## ⚙️ ETL Workflow

### 🔹 Step 1: Data Ingestion

* Imported all CSV files into IICS as source objects

### 🔹 Step 2: Data Cleaning (Dirty Sales Data)

Applied the following rules:

* Negative quantity → converted to positive
* Zero quantity → rejected
* Negative discount → converted to positive
* Discount > 100% → rejected
* Missing unit price → rejected
* Null Store ID / Product ID → rejected
* Invalid dates → standardized to `MM/DD/YYYY`
* Duplicate transactions → identified using:

  * `TRANSACTION_ID`
  * `STORE_ID`
  * `TRANSACTION_DATE`
  * `PRODUCT_ID`

---

### 🔹 Step 3: Data Transformation

* Corrected invalid values using Expression Transformation
* Routed valid and invalid records using Router Transformation
* Captured rejection reasons for invalid records
* Performed UNION of:

  * Clean dataset
  * Cleaned dirty dataset

---

### 🔹 Step 4: Data Enrichment

* Applied Lookups:

  * Product Master → Price, Category, Brand
  * Store Master → Store Name, City, State

* Invalid lookup records were rejected

---

### 🔹 Step 5: Calculations

* **Gross Amount** = `UNIT_PRICE × QUANTITY`
* **Discount Value** = `GROSS_AMOUNT × (DISCOUNT_PERCENT / 100)`
* **Net Revenue** = `GROSS_AMOUNT - DISCOUNT_VALUE`

---

## 📊 Output Files Generated

### ✅ 1. TGT_CLEAN_SALES.csv

* Final cleaned and enriched dataset

### ❌ 2. TGT_REJECTED_SALES.csv

* Invalid records with rejection reasons

### 📊 3. TGT_CATEGORY_SUMMARY.csv

* Category-wise monthly summary:

  * Total Transactions
  * Total Quantity
  * Total Revenue

### 📉 5. TGT_LOWEST_SELLING_PRODUCT_MONTHLY.csv

* Lowest selling product per month

### 🏪 6. TGT_TOP_5_PRODUCTS_PER_STORE.csv

* Top 5 products in each store

### 💰 8. TGT_HIGH_VALUE_TRANSACTIONS.csv

* Transactions where:

  * `NET_AMOUNT > Average Monthly Net Amount`

---

## 🧠 Key Concepts Used

* ETL Pipeline Design
* Data Cleaning & Validation
* Expression Transformation
* Router Transformation
* Lookup Transformation
* Union Transformation
* Aggregator Transformation
* Rank Transformation

---

## 🛠️ Tools & Technologies

* Informatica Intelligent Cloud Services (IICS)
* SQL (for database storage)
* CSV Data Handling

---

## 🚀 How to Run

1. Import CSV files into IICS
2. Create mappings as per workflow
3. Configure transformations (Expression, Router, Lookup, Union)
4. Run the mapping
5. Export final outputs to CSV

---

## 📌 Key Highlights

* Real-world ETL use case
* Data quality handling with rejection tracking
* Multi-source data integration
* Business-ready analytical outputs

---

## 👨‍💻 Author

**Rushikesh Doke, Sanket Urade, Ankur Katkamwar, Shubham Girase**
CSE (AI & ML) Students
GH Raisoni College of Engineering

---
!
