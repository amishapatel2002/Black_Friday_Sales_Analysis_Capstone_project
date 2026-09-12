# Black_Friday_Sales_Analysis_Capstone_project
Black Friday sales analysis: SQL data validation, Python EDA &amp; hypothesis testing, Power BI dashboard with business recommendations.
# 🛍️ Black Friday Sales Analysis

**End-to-end retail analytics project** — from raw transaction data to statistically validated business recommendations, built across SQL, Python, and Power BI.

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Tools](https://img.shields.io/badge/tools-Python%20%7C%20SQL%20%7C%20Power%20BI-blue)

---

## 📌 Business Context

A leading retailer with presence across metro and non-metro cities captured customer demographic and transaction data during a major Black Friday sales campaign. Leadership needed data-driven answers to:

- Which customer segments contribute most to sales, and which are underpenetrated?
- How do demographics (age, occupation, city tenure) influence purchase size and category mix?
- Which product categories dominate sales, and where do cross-sell opportunities exist?
- How can targeted campaigns and loyalty strategies retain high-value customers beyond Black Friday?

This project answers those questions using a dataset of **550,068 transactions** across **5,891 unique customers** and **3,631 unique products**.

---

## 🧰 Tools & Stack

| Stage | Tools |
|---|---|
| Data Validation | MySQL Workbench (SQL) |
| Data Cleaning & EDA | Python (Pandas, NumPy) |
| Statistical Testing | SciPy, Statsmodels |
| Visualization | Matplotlib, Seaborn |
| Dashboarding | Power BI (DAX) |

---

## 🗂️ Project Structure

```
├── sql/
│   └── black_friday_sql_checks.pdf      # Data validation queries & results
├── notebook/
│   └── black_friday_analysis.ipynb      # Full EDA, feature engineering, hypothesis testing
├── dashboard/
│   └── black_friday_dashboard.pbix      # 3-page Power BI dashboard
├── docs/
│   └── problem_statement.pdf            # Original capstone brief
└── README.md
```

---

## 🔍 Data Overview

| Column | Description |
|---|---|
| `User_ID`, `Product_ID` | Unique customer / product identifiers |
| `Gender`, `Age`, `Occupation` | Customer demographics |
| `City_Category` | City tier (A / B / C) |
| `Stay_In_Current_City_Years` | Tenure in current city |
| `Marital_Status` | 0 = Single, 1 = Married |
| `Product_Category_1/2/3` | Masked product categories (2 & 3 have missing values) |
| `Purchase` | Transaction amount (target variable) |

**Data quality note:** `Product_Category_2` is ~31.6% missing and `Product_Category_3` is ~69.7% missing. Missing values were retained as `"Unknown"` rather than imputed, and `Product_Category_3` was excluded from cross-sell analysis due to its low coverage — using it would have biased results toward the small subset of transactions with three categories filled in.

---

## ✅ Step 1 — SQL Validation

Before any analysis, the dataset was validated in MySQL Workbench:

- Row count confirmed: **550,068** (matches source file — no data lost on import)
- Null check across `User_ID`, `Product_ID`, `Purchase` — zero missing values
- Distinct counts: **5,891** unique customers, **3,631** unique products
- Spot-checked random rows to confirm data types and category formatting

---

## 📊 Step 2 — Exploratory Data Analysis (Python)

- Distribution analysis of purchase amounts, product category frequency, and city-level revenue
- Outliers in `Purchase` investigated via IQR — retained, as they represent valid high-value transactions rather than data errors
- Derived features:
  - **Customer Lifetime Value (proxy)** — total spend per customer (explicitly flagged as a proxy, not true CLV, since the dataset has no transaction dates)
  - **Category Breadth** — distinct categories purchased per customer
  - **City Loyalty Index** — average purchase × stay years

---

## 🧪 Step 3 — Hypothesis Testing

| Hypothesis | Test | Result |
|---|---|---|
| Gender affects average purchase amount | T-test | **Significant** (p < 0.05) |
| Marital status affects average purchase amount | T-test | **Not significant** (p = 0.73) |
| Age group / city category affect spending | ANOVA | Tested with documented assumptions & limitations |

Findings were reported honestly, including where correlations between demographics and purchase amount were weak (0.01–0.09) — no manufactured narrative where the data didn't support one.

---

## 🔗 Step 4 — Cross-Sell Analysis

Using `Product_Category_1` and `Product_Category_2` (excluding `Category_3` due to missing-data coverage):

- **Category 1 + 2** is the most common combination — **13.07%** of purchases
- Other strong pairings: Category 5+8, Category 5+14, Category 8+14

**Recommendation:** Bundle Category 1 + 2 for cross-sell offers.

---

## 📈 Step 5 — Power BI Dashboard (3 Pages)

**Page 1 — Executive Dashboard**
KPIs (Total Sales, Avg Purchase, Top Customer, Top Product, Top City Category), category-level purchase breakdowns, gender split, age-group spending trend, marital status distribution.

**Page 2 — Marketing Dashboard**
City-tier spending power, male vs. female spend comparison, married vs. single spend comparison, top-spending occupation groups, promotional response by category.

**Page 3 — Business Insights & Recommendations**
Plain-language summary of key findings and actionable recommendations, backed by the statistical tests above — built for stakeholders who won't read the notebook.

All filters (Gender, City_Category, Occupation, Marital_Status) are synced across pages 1 and 2 using Power BI's Sync Slicers feature, so any selection applies consistently across the whole report.

---

## 💡 Key Insights

- **26–35 age group** is the largest customer segment by transaction volume
- **City B** leads in total transactions
- **Male customers dominate** both transaction volume and spend (75.3%)
- **Gender significantly affects** purchase amount (p < 0.05); **marital status does not** (p = 0.73)
- **Category 1** drives the highest revenue, followed by Categories 5 and 8
- **Category 1 + 2** is the top cross-sell pairing (13% of purchases)

## 🎯 Recommendations

1. **Target the 26–35 segment** with personalized offers — largest, most active group
2. **Prioritize City B** for marketing spend; investigate underperformance in City A
3. **Run gender-differentiated campaigns**, backed by a statistically significant spend gap
4. **Bundle Category 1 + 2** products for cross-sell promotions
5. **Launch loyalty programs** targeting high-value repeat customers to protect concentrated revenue

---

## ⚠️ Limitations

- Dataset is **line-item grain** (one row per item purchased), not order-level — true repeat purchase rate cannot be calculated without an order ID
- No transaction dates — CLV is reported as a spend-based proxy, not a true time-weighted lifetime value
- `Occupation` and product category values are masked/anonymized by the data provider, limiting real-world interpretability of specific codes

---

## 👤 Author

**Amisha** — Data Analyst | Business Intelligence & Analytics
📍 Bhopal, India

*Data Analytics & GenAI Professional Certification — Career247*
