# Customer Segmentation and Retention Analysis

An end-to-end customer analytics project on real e-commerce transaction data — combining unsupervised segmentation, cohort retention analysis, churn prediction, and customer lifetime value (CLV) estimation to answer a core business question: **who are our most valuable customers, are we retaining them, and where should we focus effort?**

## Business Questions

1. Which customer segments drive the most revenue?
2. Are customers returning, and when are they most likely to churn?
3. Can we predict which customers are at risk of leaving?
4. What is each segment worth, and where should retention effort be focused?

## Dataset

**[Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii)** (UCI Machine Learning Repository)
- ~1.07M transactions from a UK-based online gift retailer
- Period: December 2009 – December 2011
- Raw, uncleaned transactional data — invoices, product codes, quantities, prices, customer IDs, and country

## Approach

| Phase | What it answers |
|---|---|
| 1. Data Cleaning | Removing cancellations, missing customer IDs, invalid prices/quantities |
| 2. RFM Feature Engineering | Recency, Frequency, Monetary value per customer |
| 3. Rule-Based Segmentation | Business-friendly quantile scoring (Champions, At-Risk, Lost, etc.) |
| 4. K-Means Clustering | Unsupervised validation of segments (elbow method + silhouette score) |
| 5. Segment Comparison | Cross-tabulating rule-based vs. clustering results |
| 6. Cohort Retention Analysis | Monthly retention curves by acquisition cohort |
| 7. Churn Prediction | Logistic Regression vs. Random Forest, evaluated on precision/recall/ROC-AUC |
| 8. CLV Estimation | Historical and projected 12-month customer lifetime value by segment |

## Key Findings

- **Champions** (~25% of customers) drive **69%+ of total revenue** — confirmed independently by both rule-based RFM scoring and K-Means clustering.
- Only **21.2%** of customers return within **Month 1** of their first purchase — the single largest drop-off point in the customer lifecycle.
- **Purchase Frequency** is the dominant churn signal (Logistic Regression, ROC-AUC **0.78**) — far more predictive than total spend.
- Champions carry the highest projected value (**$5,234/customer**, **$7.76M total**), while At-Risk customers still represent **~$924K** in projected value if lost.

## Business Recommendations

1. **Protect Champions** — dedicated loyalty tier, early access, personalized service.
2. **Win back At-Risk customers** — automated re-engagement at day 90/180, prioritized using the churn model's Frequency signal.
3. **Fix the Month-1 drop-off** — post-purchase email sequences targeting first-time buyers in their first 30 days.
4. **Deprioritize Lost/Inactive customers** — limit spend on this segment to low-cost channels only.

## Tech Stack

- **Python:** pandas, numpy
- **Visualization:** matplotlib, seaborn
- **Machine Learning:** scikit-learn (KMeans, LogisticRegression, RandomForestClassifier, StandardScaler)

## Repository Structure

```
customer-segmentation-retention-analysis/
├── README.md
├── requirements.txt
├── .gitignore
└── notebooks/
    └── Customer_Segmentation_and_Analytics.ipynb
```

## Data Setup

The raw dataset (~90MB) is not included in this repository to keep it lightweight. To reproduce this project:

1. Download **Online Retail II** from [UCI](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
2. Export its two sheets (`Year 2009-2010` and `Year 2010-2011`) as CSV files, or keep the original `.xlsx`
3. Place the file(s) in a local `data/` folder (this folder is git-ignored and won't be pushed)
4. Update the file path in the notebook's first data-loading cell to point to your local file

## How to Run

```bash
git clone https://github.com/faiz2517/customer-segmentation-retention-analysis.git
cd customer-segmentation-retention-analysis
pip install -r requirements.txt
jupyter notebook notebooks/Customer_Segmentation_and_Analytics.ipynb
```

Run all cells top to bottom — the notebook is organized into 10 sequential sections matching the approach table above.

## Limitations & Future Work

- CLV estimation uses a simple historical-average method; a probabilistic **BG/NBD + Gamma-Gamma** model would better account for purchase uncertainty.
- Churn features are limited to RFM-derived metrics; adding product category diversity or seasonality could improve model performance.
- An interactive dashboard (Streamlit) would make these findings explorable rather than static.

## Author

**Md Faiz Ansari**
[LinkedIn](https://www.linkedin.com/in/md-faiz-ansari-00a3a8275/)
