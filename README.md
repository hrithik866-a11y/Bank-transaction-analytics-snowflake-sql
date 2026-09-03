# Bank-transaction-analytics-snowflake-sql
Bank transaction analytics project using Snowflake SQL to analyze card spending, customer behavior, merchant performance, geographic trends, and transaction pattern

## 1. Business Problem

A bank has a large volume of transaction data but needs to understand how customers are using their cards, where spending is concentrated, which merchants generate the most transaction activity, and what spending patterns can support better business decisions.

This project uses transaction data to transform raw banking records into meaningful business insights using Snowflake SQL.

## 2. Business Objectives

The analysis aims to answer the following business questions:

* Which cards generate the highest spending?
* Which cards are used most frequently?
* Does higher transaction frequency lead to higher spending?
* How does customer spending change over time?
* Which states and cities generate the most spending?
* Which merchants have the highest transaction activity and spending?
* When are customers most active?
* Where are high-value transactions occurring?
* What are the key overall transaction KPIs?

## 3. Dataset Overview

The dataset contains **20,000 banking transactions** covering the period from **January 2023 to October 2025**.

### Key Metrics

| Metric                    |               Value |
| ------------------------- | ------------------: |
| Total Transactions        |              20,000 |
| Unique Cards              |              10,030 |
| Unique Merchants          |                 500 |
| Total Spending            |             ₹61.65M |
| Average Transaction Value |           ₹3,082.29 |
| Highest Transaction       |          ₹19,806.63 |
| Transaction Period        | Jan 2023 – Oct 2025 |

## 4. Tools & Technologies

* **Snowflake** — Data storage and SQL analysis
* **SQL** — Data cleaning, aggregation, analysis and business insights
* **GitHub** — Project documentation and version control

## 5. Data Quality Analysis

Before performing business analysis, the dataset was checked for data quality issues including:

* Record completeness
* NULL values
* Duplicate transaction IDs
* Duplicate records
* Invalid transaction amounts
* Invalid ages
* Invalid birth years
* Age and birth-year consistency
* Transaction date coverage
* Future transaction dates

The data quality checks confirmed that the dataset was suitable for further analysis.

## 6. Business Analysis

The transaction data was analyzed across the following areas:

### Card Analysis

* Most valuable cards
* Most frequently used cards
* Card usage frequency vs spending

### Spending Analysis

* Monthly spending trends
* Month-over-month spending changes
* Spending ranges
* High-value transactions

### Geographic Analysis

* State-level spending
* City-level spending
* Average transaction value by location

### Merchant Analysis

* Merchant transaction volume
* Merchant total spending
* Merchant average transaction value
* Merchant spending concentration

### Time Analysis

* Weekday vs weekend spending
* Day-of-week transaction activity

## 7. Key Business Insights

### Card Behavior

The highest-spending card generated **₹33,743.72 from only 4 transactions**, demonstrating that transaction frequency alone does not determine card value.

Low-frequency cards contributed the largest share of spending, while high-frequency cards represented a relatively small portion of the card base.

### Geographic Performance

**Maharashtra** generated the highest total spending at approximately **₹12.75M**, largely driven by its high transaction volume.

**Gujarat** recorded the highest average transaction value at approximately **₹3,128**.

At the city level, **Surat** recorded the highest total spending at approximately **₹5.45M**.

### Spending Trends

Monthly spending fluctuated throughout the analysis period rather than showing a consistent long-term upward or downward trend.

The largest month-over-month increase occurred in **March 2023 (+21.58%)**, while the largest decline occurred in **February 2023 (-17.82%)**.

### Time-Based Behavior

Weekdays accounted for the majority of transactions and spending.

**Sunday** recorded the highest total spending among individual days, while **Tuesday** recorded the highest average transaction value.

### High-Value Transactions

Transactions above **₹10,000** were analyzed to understand high-value spending behavior.

**Maharashtra** recorded the highest number of high-value transactions, while the largest individual transaction was **₹19,806.63 in Uttar Pradesh**.

## 8. Business Recommendations

Based on the analysis:

1. **Target high-value cardholders** with premium rewards and personalized offers rather than relying only on transaction frequency.
2. **Focus regional strategies** on high-spending markets such as Maharashtra and high-average-value markets such as Gujarat.
3. **Strengthen merchant partnerships** with merchants generating consistently high transaction volumes and spending.
4. **Use spending patterns for campaign timing**, particularly around periods and days with higher transaction activity.
5. **Monitor high-value transactions** as a separate segment for deeper customer and transaction-level analysis.

## 9. Project Structure

```text
bank-transaction-analytics-snowflake-sql/
│
├── README.md
│
└── bank_transaction_analysis.sql
```

## 10. Conclusion

This project demonstrates how Snowflake SQL can be used to move from raw transaction data to actionable business insights.

The analysis highlights card spending behavior, transaction frequency, geographic performance, merchant activity, time-based patterns, and high-value transactions to support data-driven banking decisions.
