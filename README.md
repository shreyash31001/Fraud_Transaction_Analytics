# Payment Fraud & Risk Analytics

## Overview

This project analyzes payment transaction behavior and fraud risk using the **BankSim synthetic banking payment dataset**.

The objective is to approach payment fraud from the perspective of a financial institution: not simply identifying fraudulent transactions, but understanding **where financial exposure is concentrated, which merchants and customers exhibit elevated risk, and how fraudulent activity differs from normal payment behavior**.

The analysis was developed in **Power BI** with a focus on business-oriented risk metrics and interactive reporting.

---

## Business Problem

Financial institutions process large volumes of payment transactions, making it difficult to manually identify where fraud risk is concentrated.

The key questions addressed in this analysis are:

1. What is the overall scale and value of payment activity?
2. What proportion of transactions are fraudulent?
3. How much financial exposure is associated with fraudulent transactions?
4. Which merchant categories and merchants exhibit elevated fraud risk?
5. Which customers have unusually high fraudulent activity?
6. Are fraudulent transactions materially different from normal transactions?
7. Does fraud activity vary over time or across customer segments?

The goal is to transform transaction-level data into information that could support **fraud monitoring, risk prioritization, and management decision-making**.

---

## Dataset

The project uses the **BankSim synthetic payment dataset**, generated using an agent-based simulator calibrated from aggregated transactional data provided by a bank in Spain.

The dataset contains approximately:

* **594,643 transactions**
* **587,443 normal transactions**
* **7,200 fraudulent transactions**
* **4,112 unique customers**
* **50 merchants**
* **15 merchant categories**
* Approximately **180 simulation steps**

The overall simulated fraud rate is approximately **1.21%**.

Because BankSim is synthetic, the analysis should not be interpreted as evidence of actual banking or demographic behavior. Its purpose is to demonstrate the analytical framework and techniques used to investigate payment fraud.

---

## Key Metrics

### Payment Activity

**Total Transactions**

Number of payment transactions processed.

**Total Transaction Value**

Total monetary value of all transactions.

```DAX
Total Transaction Value =
SUM(BankSim[amount])
```

**Average Transaction Value**

Average monetary value per transaction.

```DAX
Average Transaction Value =
AVERAGE(BankSim[amount])
```

### Fraud Risk

**Fraudulent Transactions**

Number of transactions where the fraud indicator equals 1.

```DAX
Fraud Transactions =
CALCULATE(
    COUNTROWS(BankSim),
    BankSim[fraud] = 1
)
```

**Fraud Rate**

Percentage of all transactions classified as fraudulent.

```DAX
Fraud Rate =
DIVIDE(
    [Fraud Transactions],
    [Total Transactions]
)
```

**Fraud Amount**

Total transaction value associated with fraudulent transactions.

```DAX
Fraud Amount =
CALCULATE(
    SUM(BankSim[amount]),
    BankSim[fraud] = 1
)
```

### Customer-Level Metrics

**Total Transactions**

```DAX
Total Transactions =
COUNTROWS(BankSim)
```

**Total Customer Spending**

```DAX
Total Customer Spending =
SUM(BankSim[amount])
```

**Fraud Transactions per Customer**

```DAX
Fraud Transactions =
CALCULATE(
    COUNTROWS(BankSim),
    BankSim[fraud] = 1
)
```

**Customer Fraud Rate**

```DAX
Customer Fraud Rate =
DIVIDE(
    [Fraud Transactions],
    [Total Transactions]
)
```

These metrics allow customer activity to be evaluated from both a **frequency** and **financial exposure** perspective.

---

## Dashboard Structure

### 1. Payment Overview

The overview dashboard establishes the scale of the payment system and provides a high-level view of fraud exposure.

Key metrics and analyses include:

* Total transactions
* Total transaction value
* Fraudulent transactions
* Fraud rate
* Fraud amount
* Unique customers
* Transaction volume over time
* Transaction activity by category
* Transaction amount distribution

---

### 2. Fraud Risk Analysis

This section focuses on identifying where fraud risk is concentrated.

Analyses include:

* Fraud rate by merchant category
* Top merchants by fraud rate
* Merchant transaction volume
* Fraud amount by merchant
* Fraud amount by category
* Fraudulent activity over time
* Comparison of fraudulent and normal transaction amounts

A key consideration is distinguishing **fraud frequency** from **financial exposure**.

For example, a merchant with a high fraud rate but only a handful of transactions may represent less overall exposure than a high-volume merchant with a moderately elevated fraud rate.

---

### 3. Customer Risk Analysis

The customer analysis examines fraud from an individual customer perspective.

Key analyses include:

* Top 5 customers by fraudulent transactions
* Top 5 customers by fraud amount
* Customer spending vs. fraudulent transactions
* Customer transaction frequency
* Fraud rate by gender
* Fraud rate by age group

The objective is to identify customers whose transaction behavior may warrant additional investigation or monitoring.

---

## Analytical Approach

The project follows a business-oriented analytical workflow:

```text
Transaction Data
       ↓
Data Profiling & Validation
       ↓
Payment Activity Analysis
       ↓
Fraud Rate & Financial Exposure
       ↓
Merchant Risk Analysis
       ↓
Customer Risk Analysis
       ↓
Behavioral Comparison
       ↓
Management Insights
```

Rather than relying on a single fraud metric, the analysis considers:

**Volume + Frequency + Monetary Exposure + Concentration + Customer Behavior**

This helps avoid misleading conclusions based on raw fraud counts alone.

---

## Key Analytical Considerations

### Fraud Rate vs. Fraud Count

A merchant with the largest number of fraudulent transactions is not necessarily the highest-risk merchant.

Fraud rate must be evaluated alongside transaction volume.

### Fraud Frequency vs. Financial Exposure

The customer with the highest number of fraudulent transactions may not have the greatest financial exposure.

Therefore, both:

* Fraudulent transaction count
* Fraud amount

are evaluated.

### Class Imbalance

Fraudulent transactions represent approximately **1.21%** of the dataset.

This means that normal transactions heavily outnumber fraudulent transactions and that raw transaction counts can be misleading when comparing risk.

### Synthetic Data

BankSim is a simulated dataset. Observed relationships should therefore be treated as analytical demonstrations rather than claims about real-world banking customers, merchants, or demographics.

---

## Tools & Technologies

**Business Intelligence**

* Power BI
* Power Query
* DAX

**Analytics**

* Descriptive statistics
* Segmentation
* Fraud-rate analysis
* Customer-level aggregation
* Merchant risk analysis
* Trend analysis

**Data**

* BankSim synthetic payment dataset

---

## DAX Measures

### Total Transactions

```DAX
Total Transactions =
COUNTROWS(BankSim)
```

### Total Transaction Value

```DAX
Total Transaction Value =
SUM(BankSim[amount])
```

### Average Transaction Value

```DAX
Average Transaction Value =
AVERAGE(BankSim[amount])
```

### Fraud Transactions

```DAX
Fraud Transactions =
CALCULATE(
    COUNTROWS(BankSim),
    BankSim[fraud] = 1
)
```

### Fraud Rate

```DAX
Fraud Rate =
DIVIDE(
    [Fraud Transactions],
    [Total Transactions]
)
```

### Fraud Amount

```DAX
Fraud Amount =
CALCULATE(
    SUM(BankSim[amount]),
    BankSim[fraud] = 1
)
```

### Unique Customers

```DAX
Unique Customers =
DISTINCTCOUNT(BankSim[customer])
```

### Customer Fraud Rate

```DAX
Customer Fraud Rate =
DIVIDE(
    [Fraud Transactions],
    [Total Transactions]
)
```

---

## Management Perspective

The central objective of this project is not simply to identify fraudulent transactions.

A more useful management perspective is:

> **Where is fraud risk concentrated, how significant is the associated financial exposure, and where should monitoring or investigative resources be prioritized?**

This requires moving beyond transaction counts toward a combination of:

* Fraud rate
* Fraud amount
* Transaction volume
* Merchant concentration
* Customer behavior
* Transaction characteristics
* Temporal patterns

The resulting dashboard provides a framework for turning transaction-level payment data into **risk-oriented business intelligence**.

---

## Limitations

* The dataset is synthetic and does not represent actual customer transactions.
* The dataset contains a limited number of merchants and customer attributes.
* Demographic variables should not be interpreted as causal explanations for fraud.
* Correlation between transaction characteristics and fraud does not establish causation.
* The dashboard is designed for descriptive and diagnostic analytics rather than production fraud detection.

---

## Dataset Reference

The dataset is based on the BankSim research project:

**Lopez-Rojas, Edgar Alonso & Axelsson, Stefan.**
*BankSim: A bank payments simulator for fraud detection research.*
26th European Modeling and Simulation Symposium (EMSS), 2014.

The BankSim dataset was developed to provide synthetic payment data for fraud detection research while avoiding disclosure of private customer transactions.

---

## Project Objective

This project demonstrates how transaction-level payment data can be transformed into an interactive fraud-risk reporting solution that connects:

**Operational payment activity → Fraud exposure → Risk concentration → Customer & merchant analysis → Management decision support.**
