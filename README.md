# Bank Transaction Analytics Using Snowflake SQL

## 1. Business Problem

A bank has a large volume of transaction data but needs to understand how customers are using their cards, where spending is concentrated, which merchants generate the most transaction activity, and what spending patterns can support better business decisions.

This project uses **Snowflake SQL** to transform raw banking transaction data into meaningful business insights.

---

## 2. Business Objectives

The project aims to answer the following business questions:

* Which cards generate the highest spending?
* Which cards are used most frequently?
* Does higher transaction frequency lead to higher spending?
* Which merchants generate the most transaction activity?
* Which merchants account for the highest spending?
* Which states and cities generate the most spending?
* How does spending change over time?
* Are customers more active on weekdays or weekends?
* Which days have the highest transaction activity?
* Where are high-value transactions concentrated?
* What are the overall transaction and spending KPIs?

---

## 3. Dataset Overview

The dataset contains banking card transaction records.

### Dataset Statistics

| Metric                    |      Value |
| ------------------------- | ---------: |
| Total Transactions        |     20,000 |
| Unique Cards              |     10,030 |
| Unique Merchants          |        500 |
| Total Spending            |    ₹61.65M |
| Average Transaction Value |  ₹3,082.29 |
| Highest Transaction       | ₹19,806.63 |
| First Transaction         | 2023-01-01 |
| Last Transaction          | 2025-10-31 |

### Important Columns

* `TRANSACTION_ID` – Unique transaction identifier
* `CARD_ID` – Card identifier
* `AMOUNT` – Transaction amount
* `DATE` – Transaction date
* `MERCHANT_ID` – Merchant identifier
* `MERCHANT_CITY` – Merchant location
* `MERCHANT_STATE` – Merchant state
* `CURRENT_AGE` – Customer age
* `BIRTH_YEAR` – Customer birth year

> Note: The dataset does not contain a `CUSTOMER_ID`. Therefore, `CARD_ID` is used as the primary identifier for card-level behavioral analysis.

---

## 4. Snowflake Data Setup

The transaction dataset was loaded into **Snowflake** for data preparation, validation, and SQL-based analysis.

### Database Structure

```text
BANK_ANALYTICS
└── RAW_DATA
    └── TRANSACTIONS
```

### Data Preparation

The dataset was:

* Loaded into Snowflake
* Stored in the `RAW_DATA` schema
* Validated for NULL values
* Checked for duplicate records
* Checked for invalid transaction amounts
* Validated customer age and birth year
* Checked transaction date coverage
* Checked for future transaction dates

---

## 5. Data Quality Analysis

Before performing business analysis, the dataset was validated to ensure the transaction records were suitable for analysis.

### Checks Performed

#### NULL Value Check

Checked important fields including:

* `CARD_ID`
* `TRANSACTION_ID`
* `AMOUNT`
* `MERCHANT_ID`
* `MERCHANT_CITY`
* `MERCHANT_STATE`

**Result:** No NULL values were identified in the checked fields.

#### Transaction Amount Validation

Checked for zero or negative transaction amounts.

| Metric               |     Result |
| -------------------- | ---------: |
| Minimum Amount       |    ₹105.16 |
| Maximum Amount       | ₹19,806.63 |
| Non-Positive Amounts |          0 |

**Insight:** All transaction amounts are positive and fall within the observed range.

#### Age Validation

Customer ages were checked for unrealistic values.

**Result:** No invalid ages were identified.

#### Birth Year Validation

Birth years were checked for unrealistic values.

**Result:** No invalid birth years were identified.

#### Age vs Birth Year Consistency

Customer age was compared against birth year to identify inconsistencies.

**Result:** No inconsistencies were identified based on the validation logic.

#### Transaction Date Validation

The transaction date range was checked.

* Earliest transaction: **2023-01-01**
* Latest transaction: **2025-10-31**
* Unique transaction dates: **1,035**

**Result:** The dataset covers transactions across multiple years.

---

## 6. Business Analysis

### 6.1 Card Analysis

Card-level analysis was performed to understand customer/card spending behavior.

#### Key Analyses

* Top cards by total spending
* Card transaction frequency
* Spending by usage frequency
* Average transaction value by usage group

### Key Insight

Most spending comes from **low- and medium-frequency cards**, while high-frequency cards represent a relatively small portion of the card base.

High-frequency cards also have a slightly lower average transaction value, suggesting that **frequent card usage does not necessarily result in higher-value transactions**.

---

### 6.2 Merchant Analysis

Merchant-level analysis was performed to identify merchants with the highest transaction activity and spending.

#### Key Analyses

* Top merchants by transaction volume
* Top merchants by total spending
* Spending concentration among the top 10 merchants
* Merchant performance by city and state

### Key Insight

Merchant activity is distributed across a large number of merchants rather than being dominated by a small number of merchants.

---

### 6.3 Geographic Analysis

Transaction activity was analyzed across states and cities.

#### Top State by Spending

**Maharashtra**

* Transactions: 4,132
* Total spending: ₹12.75M
* Average transaction: ₹3,085.16

#### Top City by Spending

**Surat**

* Transactions: 1,761
* Total spending: ₹5.45M
* Average transaction: ₹3,094.01

#### Highest Average Transaction Value

Among the major cities analyzed, **Ahmedabad** had the highest average transaction value at approximately **₹3,175.71**.

### Key Insight

Maharashtra leads overall spending largely because of its higher transaction volume, while Gujarat shows strong average transaction values.

---

### 6.4 Spending Analysis

Transaction amounts were grouped into spending ranges to understand the distribution of transaction sizes.

The analysis also examined monthly spending patterns.

#### Monthly Analysis

Monthly spending was calculated using `DATE_TRUNC()` to aggregate individual transaction dates into monthly periods.

Month-over-month spending changes were also calculated using the `LAG()` window function.

### Key Insight

Monthly spending fluctuates over time rather than following a consistent long-term upward or downward trend.

The largest monthly increase observed was approximately **21.58%**, while the largest decline was approximately **17.82%**.

---

### 6.5 Time-Based Analysis

Transaction activity was compared between weekdays and weekends.

| Day Type | Transactions | Total Spending | Avg Transaction |
| -------- | -----------: | -------------: | --------------: |
| Weekday  |       17,150 |        ₹53.05M |       ₹3,093.41 |
| Weekend  |        2,850 |         ₹8.59M |       ₹3,015.36 |

### Key Insight

Weekdays account for the majority of transaction activity and spending.

Among individual days:

* **Sunday** had the highest total spending.
* **Tuesday** had the highest average transaction value.
* **Monday** had the lowest average transaction value.

---

### 6.6 High-Value Transaction Analysis

Transactions of **₹10,000 or more** were analyzed separately to understand high-value spending patterns.

### Key Findings

* Maharashtra had the highest number of high-value transactions.
* Uttar Pradesh contained the highest individual transaction at **₹19,806.63**.
* Karnataka had the highest average transaction value among the states with high-value transactions.

> High-value transactions are not automatically considered fraudulent. This analysis only identifies large-value transactions for business analysis.

---

## 7. Key Business Insights

The analysis produced the following major insights:

### 1. Spending is concentrated among low- and medium-frequency cards

The majority of total spending comes from cards with relatively low or medium transaction frequency.

### 2. Transaction frequency does not guarantee higher transaction value

High-frequency cards have a slightly lower average transaction value compared with low- and medium-frequency cards.

### 3. Maharashtra is the leading state

Maharashtra generates the highest transaction volume and total spending in the dataset.

### 4. Surat is the leading city by spending

Surat records the highest total spending among the cities analyzed.

### 5. Weekdays dominate transaction activity

Most transactions and spending occur during weekdays.

### 6. Spending varies considerably month to month

Monthly spending shows fluctuations rather than a consistent growth trend.

### 7. High-value transactions are geographically distributed

Large transactions occur across multiple states, with Maharashtra having the highest number of transactions above ₹10,000.

---

## 8. Business Recommendations

Based on the analysis, the bank could consider the following actions:

### Customer Engagement

Target low- and medium-frequency cardholders with personalized offers and campaigns to encourage increased card usage.

### High-Value Customer Programs

Identify cards with consistently high total spending and consider premium rewards or loyalty programs.

### Geographic Campaigns

Focus marketing and card acquisition strategies on high-performing states and cities such as Maharashtra, Gujarat, and Surat.

### Merchant Partnerships

Explore partnerships with high-volume and high-spending merchants to develop cashback, rewards, or co-branded campaigns.

### Transaction Monitoring

Use high-value transaction analysis as one input into transaction monitoring and risk-analysis systems, while combining it with additional behavioral and fraud-related signals.

---

## 9. Project Structure

bank-transaction-analytics-snowflake-sql/
│
├── README.md
├── bank_transaction_analysis.sql
│
└── screenshots/
    ├── overall_kpis
    └── geographic_analysis



```

### SQL File Structure

```text
00. DATABASE & TABLE SETUP
01. DATA QUALITY
02. CARD ANALYSIS
03. MERCHANT ANALYSIS
04. GEOGRAPHIC ANALYSIS
05. SPENDING ANALYSIS
06. TIME-BASED ANALYSIS
07. HIGH-VALUE TRANSACTION ANALYSIS
08. OVERALL KPIs
```

---

## 10. Technologies Used

* **Snowflake** – Data storage and SQL analysis
* **SQL** – Data validation, transformation, aggregation, and analysis
* **GitHub** – Project documentation and version control

---

## 11. Conclusion

This project demonstrates how **Snowflake SQL** can be used to transform raw banking transaction data into actionable business insights.

The analysis covers data quality validation, card behavior, merchant performance, geographic spending, transaction trends, time-based patterns, high-value transactions, and overall business KPIs.

The project demonstrates practical SQL skills including:

* Aggregations
* `GROUP BY`
* `CASE` statements
* CTEs
* Window functions
* `LAG()`
* Date functions
* `DATE_TRUNC()`
* Data quality validation
* Business KPI analysis

The findings can support decisions related to **customer engagement, merchant partnerships, geographic targeting, and transaction monitoring**.

