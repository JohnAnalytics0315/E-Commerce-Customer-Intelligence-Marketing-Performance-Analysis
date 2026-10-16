# E-Commerce Customer Intelligence & Marketing Performance Analysis

End-to-end marketing analytics project using the **UCI Online Retail II** dataset (1M+ transactions, 5,800+ customers across 40 countries). Demonstrates a full customer analytics pipeline — from raw transactional data to actionable segmentation, retention insights, and predictive modeling.

---

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Analyses](#analyses)
  - [1. RFM Segmentation & K-Means Clustering](#1-rfm-segmentation--k-means-clustering)
  - [2. Cohort Retention Analysis](#2-cohort-retention-analysis)
  - [3. Marketing Channel Attribution](#3-marketing-channel-attribution)
  - [4. Campaign A/B Test Analysis](#4-campaign-ab-test-analysis)
  - [5. Customer Lifetime Value (CLV) Prediction](#5-customer-lifetime-value-clv-prediction)
- [Key Findings](#key-findings)
- [Tech Stack](#tech-stack)
- [How to Run](#how-to-run)
- [Project Structure](#project-structure)
- [Author](#author)

---

## Overview

This project tackles five core marketing analytics problems that businesses face daily:

- **Who are our best customers?** → RFM Segmentation + K-Means Clustering
- **Are we retaining customers over time?** → Cohort Retention Analysis
- **Which channels bring the most valuable customers?** → Channel Attribution
- **Does our campaign actually work?** → A/B Test with Statistical Rigor
- **How much will a customer spend in the future?** → CLV Prediction via Ridge Regression

Each analysis is self-contained with its own visualizations and interpretation, but together they form a complete customer intelligence framework.

## Dataset

| Detail | Value |
|:-------|:------|
| **Source** | [UCI Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii) |
| **Records** | 1,067,371 transactions |
| **Customers** | ~5,800 unique (after cleaning) |
| **Period** | December 2009 – December 2011 |
| **Countries** | 40 |
| **Business** | UK-based non-store online retailer (wholesale) |

**Columns:** `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, `Country`

> **Note:** The dataset does not include marketing channel or campaign data. `AcquisitionChannel` and `CampaignVariant` are engineered fields assigned per customer using realistic distributions to demonstrate attribution and A/B testing methodology. This is clearly documented in the notebook.

## Analyses

### 1. RFM Segmentation & K-Means Clustering

Computed **Recency**, **Frequency**, and **Monetary** value per customer, standardized the features, and applied K-Means clustering. Used the Elbow Method and Silhouette Score to evaluate cluster quality.

**Output:** Four customer segments — Champions, Promising, At Risk, and Hibernating — each with distinct behavioral profiles and targeted marketing recommendations.

### 2. Cohort Retention Analysis

Grouped customers by their **first purchase month** and tracked the percentage returning in each subsequent month. Produced a retention heatmap and an average retention curve.

**Output:** Monthly cohort retention heatmap revealing the critical drop-off window (Month 1-2), highlighting where onboarding interventions would have the highest impact.

### 3. Marketing Channel Attribution

Analyzed five acquisition channels (Organic Search, Paid Social, Email, Direct, Referral) across four metrics: total revenue, revenue per customer, repeat purchase rate, and average order value.

**Output:** Four-panel attribution dashboard showing which channels deliver volume vs. long-term customer value.

### 4. Campaign A/B Test Analysis

Compared two campaign variants using:

- **Welch's t-test** (unequal variances)
- **Cohen's d** (effect size)
- **95% confidence interval** for the mean difference

**Output:** Complete statistical report with revenue distribution histograms and box plots, including a clear significant/not-significant verdict.

### 5. Customer Lifetime Value (CLV) Prediction

Split the dataset at the midpoint (January 2011). Used the first period to compute RFM features + Tenure + Average Order Value, then predicted the holdout period's actual revenue using **Ridge Regression** with 5-fold cross-validation.

| Metric | Value |
|:-------|:------|
| Cross-validated R² | 0.593 ± 0.021 |
| Model | Ridge (α=10) |
| Features | Recency, Frequency, Monetary, Tenure, AvgOrderValue |

**Output:** Feature importance chart, actual vs. predicted scatter plot, and CLV tier summary (Low / Medium / High / VIP).

## Key Findings

| Analysis | Insight |
|:---------|:--------|
| **RFM Segmentation** | Customers cluster into 4 distinct segments. Champions (high frequency, high spend, recent activity) represent the highest-value group for loyalty programs. |
| **Cohort Retention** | Retention drops sharply after Month 1 — the first-repeat window is the highest-leverage intervention point for reducing churn. |
| **Channel Attribution** | Organic Search and Email drive the highest revenue per customer and repeat rates, making them the most efficient long-term channels. |
| **A/B Test** | Small effect sizes suggest marginal creative differences between variants — bolder variations (offers, landing pages) should be tested next. |
| **CLV Prediction** | Frequency and Monetary value are the strongest predictors of future revenue. VIP-tier customers generate disproportionate returns. |

## Tech Stack

| Category | Tools |
|:---------|:------|
| **Language** | Python 3 |
| **Data** | pandas, NumPy |
| **Machine Learning** | scikit-learn (KMeans, Ridge, StandardScaler) |
| **Statistics** | SciPy (Welch's t-test) |
| **Visualization** | Matplotlib, Seaborn |
| **Environment** | Jupyter Notebook |

## How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/JohnAnalytics0315/ecommerce-marketing-analysis.git
   cd ecommerce-marketing-analysis
   ```

2. **Install dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn scipy openpyxl
   ```

3. **Download the dataset:**

   Download `online_retail_II.xlsx` from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/502/online+retail+ii) and place it in the same directory as the notebook.

4. **Run the notebook:**
   ```bash
   jupyter notebook ecommerce_marketing_analysis.ipynb
   ```

## Project Structure

```
├── ecommerce_marketing_analysis.ipynb   # Full analysis notebook (36 cells)
├── online_retail_II.xlsx                # UCI Online Retail II dataset
└── README.md                           # This file
```

## Author

**Bogart Caligonan**
- GitHub: [@JohnAnalytics0315](https://github.com/JohnAnalytics0315)

---

*Dataset citation: Daqing Chen (2019). Online Retail II. UCI Machine Learning Repository. https://doi.org/10.24432/C5CG6D*
