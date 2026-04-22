# Chicago Traffic Crash Analysis — Injury Risk Modeling & EDA

End-to-end analysis of 1M+ traffic crash records from Chicago (2013–2025), combining statistical EDA, hypothesis testing, and a logistic regression injury prediction model to identify key risk factors for crash severity.

---

## Problem Statement

Traffic crashes impose enormous public health and economic costs on urban communities. Despite the availability of large-scale crash datasets, granular record-level analysis is rarely applied to inform safety policy. This project leverages Chicago's open crash data to uncover when, where, and under what conditions crashes are most likely to result in injuries — and builds a predictive model to quantify those risks.

---

## Dataset

- **Source:** [Chicago Traffic Crashes — Chicago Data Portal (data.gov)](https://catalog.data.gov/dataset/traffic-crashes-crashes)
- **Origin:** Chicago Police Department (CPD)
- **Scale:** 1,029,797 crash records · 48 columns · 2013–2025
- **Target variable:** Binary injury indicator (injury vs. no injury)

---

## Project Pipeline

**1. Data Cleaning & Preparation**
- Dropped columns with >95% missing values (WORKERS_PRESENT_I, DOORING_I, WORK_ZONE_TYPE, etc.)
- Mixed imputation strategy: median for continuous variables, mode for categoricals, zero-fill for injury counts
- Datetime parsing and extraction of crash year, weekday, and week number
- Binary indicator normalization (Y/YES/TRUE → 1) and safe numeric coercion
- Final cleaned dataset: 1,029,797 records · 42 columns

**2. Exploratory Data Analysis**
- Monthly crash trends with 12-month rolling mean and standard deviation
- Crash frequency by hour of day, day of week, and weather condition
- Injury probability estimates with 95% confidence intervals
- Speed limit vs. injury probability correlation analysis (aggregated and record-level)
- Top contributing causes of crashes

**3. Statistical Testing**
- Z-test for weekday vs. weekend injury rate difference (Z = 9.532)
- Conditional injury probability by weather category (≥500 cases)
- Confidence interval: injury probability = 0.1432 (95% CI: 0.1425–0.1438)

**4. Predictive Modeling**
- Logistic regression with scikit-learn pipeline (StandardScaler + OneHotEncoder + LogisticRegression)
- Stratified 80/20 train-test split
- Feature importance via coefficient analysis

---

## Key Findings

| Factor | Insight |
|---|---|
| **Crash type** | Pedestrian crashes carry the highest injury coefficient (+3.41), followed by cyclist (+2.26) and rollover (+0.74) |
| **Speed** | Aggregated injury probability vs. speed limit shows r = 0.922; record-level r = 0.081 — grouping reveals hidden patterns |
| **Time of day** | Peak crash hour is 15:00 (80,013 crashes); overnight hours (2–5 AM) are lowest |
| **Weather** | Blowing snow (19.2%) and fog/haze (18.2%) have the highest injury probability |
| **Weekends** | Weekend injury rate (14.85%) is slightly but significantly higher than weekdays (14.11%) |
| **Overall injury rate** | 14.32% of all crashes result in injury; fatal crashes are 0.106% |

**Model Performance:** Logistic Regression ROC-AUC ≈ **0.78–0.79**

---

## Tech Stack

| Area | Tools |
|---|---|
| Data Processing | Python, Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Statistical Testing | SciPy (z-tests, confidence intervals) |
| Modeling | Scikit-learn (LogisticRegression, ColumnTransformer, Pipeline) |

---

*IE7275 – Data Mining in Engineering | Group 2*
