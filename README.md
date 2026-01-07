Here’s a clean, professional **GitHub `README.md`** tailored for your **Cafe Sales Data Cleaning Pipeline** project. It’s written to look solid for recruiters, reviewers, and collaborators, and aligns well with data engineering / data science best practices.

---

# ☕ Cafe Sales Data Cleaning Pipeline

A robust data cleaning and validation pipeline for messy transactional cafe sales data.
This project focuses on **auditing**, **standardizing**, **imputing**, and **validating** real-world dirty data using Python, Pandas, and NumPy.

---

## 📌 Project Overview

Real-world datasets are rarely clean. This project demonstrates a practical, production-style data cleaning workflow applied to a raw cafe transaction dataset (`dirty_cafe_sales.csv`).

The pipeline:

* Standardizes inconsistent missing values
* Fixes incorrect data types
* Recovers missing numerical values using mathematical relationships
* Tracks inferred values transparently
* Validates final data integrity

The final output is a **clean, analysis-ready dataset** suitable for reporting, visualization, or downstream machine learning tasks.

---

## 📊 Dataset Information

* **Input File:** `https://www.kaggle.com/datasets/ahmedmohamed2003/cafe-sales-dirty-data-for-cleaning-training`
* **Rows:** 10,000
* **Columns:** 8

### Key Columns

| Column Name      | Description                   |
| ---------------- | ----------------------------- |
| Transaction ID   | Unique transaction identifier |
| Item             | Product name                  |
| Quantity         | Units sold                    |
| Price Per Unit   | Price per item                |
| Total Spent      | Total transaction value       |
| Payment Method   | Cash, Card, etc.              |
| Location         | Store location                |
| Transaction Date | Date of transaction           |

---

## 🚨 Identified Data Quality Issues

The raw dataset contained multiple real-world data issues:

* Inconsistent null values (`NaN`, `"UNKNOWN"`, `"ERROR"`)
* Numeric columns stored as strings
* Invalid date values
* Missing values across Quantity, Price, and Total Spent
* Logical inconsistencies between Quantity × Price ≠ Total

---

## 🧹 Cleaning Methodology

### 1️⃣ Categorical Standardization

Applied to:

* `Item`
* `Payment Method`
* `Location`

**Action:**

* Unified `"UNKNOWN"`, `"ERROR"`, and missing values into a single category: `"Unknown"`

---

### 2️⃣ Numerical Formatting

Applied to:

* `Quantity`
* `Price Per Unit`
* `Total Spent`

**Action:**

* Replaced `"ERROR"` and `"UNKNOWN"` with `NaN`
* Converted columns from `object` to `float`

---

### 3️⃣ Date Parsing

* Converted `Transaction Date` to `datetime`
* Invalid values were safely coerced to `NaT`

---

## 🔁 Missing Value Imputation Logic

Missing numerical values were **recovered mathematically** using the core relationship:

```
Total Spent = Quantity × Price Per Unit
```

To ensure transparency, the pipeline tracks inferred values using boolean flags.

### ✔ Inference Rules

#### 1. Inferring Quantity

* **Condition:** Total Spent and Price Per Unit are known
* **Formula:**

  ```
  Quantity = Total Spent / Price Per Unit
  ```

#### 2. Inferring Price Per Unit

* **Condition:** Total Spent and Quantity are known
* **Formula:**

  ```
  Price Per Unit = Total Spent / Quantity
  ```

#### 3. Inferring Total Spent

* **Condition:** Quantity and Price Per Unit are known
* **Formula:**

  ```
  Total Spent = Quantity × Price Per Unit
  ```

### 🏷 Inference Tracking Columns

* `Quantity_Inferred`
* `Price_Per_Unit_Inferred`
* `Total_Spent_Inferred`

---

## ✅ Data Validation

A final consistency check ensures mathematical correctness:

* **Column Added:** `Total_Spent_Valid` (Boolean)
* **Logic:**

  ```
  abs((Quantity × Price Per Unit) - Total Spent) <= 0.01
  ```
* Rows with unresolved or inconsistent values are flagged as `False`

---

## 📤 Output

* **File:** `cleaned_data.csv`
* **Includes:**

  * Cleaned original columns
  * Inference tracking flags
  * Validation column

The resulting dataset is **fully analysis-ready**.

---

## 🧪 Technologies Used

* Python 3.x
* Pandas
* NumPy
* Jupyter Notebook

---

## 🚀 How to Run

```bash
pip install pandas numpy
```

Open and run the notebook:

```bash
jupyter notebook cafe-sales-practice.ipynb
```

---

## 🎯 Skills Demonstrated

* Real-world data cleaning
* Data auditing & validation
* Feature engineering
* Missing value imputation
* Defensive data processing
* Reproducible data pipelines

---

## 📄 License

This project is for educational and portfolio purposes.

---

If you want, next I can:

* Add **project screenshots**
* Convert this into a **portfolio-ready case study**
* Rewrite it for **Kaggle / LinkedIn / resume bullets**
* Add **data quality metrics** (before vs after)

Just say the word.
