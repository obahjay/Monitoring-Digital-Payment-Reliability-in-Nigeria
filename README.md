# Monitoring-Digital-Payment-Reliability-in-Nigeria
### Analyzing digital payment reliability, identify transaction patterns, measure account-level concentration, and evaluate monitoring KPIs through controlled scenario simulations.

**PairBud Project:**  Emmanuel Olawumi and Favour Obajuaye

---

## 1. Project Overview

This project explores how data analytics can support the monitoring of digital payment reliability using a synthetic Nigerian retail banking transaction dataset.

It examines transaction outcomes, account-level activity, transaction volume patterns, and activity distribution across payment channels, merchant categories, and geographical locations.

The project also uses controlled scenario simulations to evaluate how selected monitoring indicators respond to changes in transaction outcomes.

The main objective is to demonstrate a reproducible analytical workflow and translate findings into practical transaction monitoring recommendations.

**Note:** The dataset is synthetic. Findings describe only the generated data and do not represent the actual performance of Nigerian banks, fintech companies, or payment systems.

## 2. Problem Statement

Failed, pending, and reversed transactions can create operational challenges for financial institutions and payment providers.

Effective monitoring requires indicators that help operations teams identify unusual changes in transaction outcomes and activity patterns.

Due to limited publicly available transaction-level banking data, this project uses synthetic data to demonstrate transaction profiling, scenario simulations, and KPI-based monitoring.

The project does not investigate the causes of payment failures because the dataset does not contain failure reason codes or the operational information required for causal analysis.

## 3. Project Aim and Objectives

### Aim

To profile transaction activity in a synthetic Nigerian retail banking dataset and evaluate monitoring KPIs under explicitly defined reliability scenarios.

### Objectives

- Examine successful, failed, pending, and reversed transactions.
- Measure transaction concentration across customer accounts.
- Analyse transaction volume and temporal patterns.
- Examine transaction distribution across channels, merchant categories, and states.
- Investigate data quality and document variables unsuitable for analysis.
- Simulate controlled changes in transaction outcomes.
- Evaluate monitoring methods using detection and false-alert measures.
- Recommend practical KPIs for transaction reliability monitoring.

## 4. Dataset and Sources

### Primary Dataset

**Nigerian Banking Retail Transactions**

- Source: [Hugging Face Dataset Repository](https://huggingface.co/datasets/electricsheepafrica/nigerian-banking-retail-transactions)
- [Download Parquet Dataset](https://huggingface.co/datasets/electricsheepafrica/nigerian-banking-retail-transactions/resolve/main/nigerian_retail_transactions_full.parquet)

| Attribute | Description |
|---|---|
| Records | 5,000,000 |
| Original columns | 16 |
| Period | January 2023 – December 2024 |
| Coverage | 730 calendar days |
| Currency | Nigerian Naira (NGN) |
| Format | Parquet |
| Data type | Synthetic transaction data |

The dataset contains transaction timestamps, amounts, transaction types, payment channels, merchant information, geographical locations, transaction statuses, account identifiers, and a synthetic fraud indicator.

### External Context

[Central Bank of Nigeria – e-Payment Statistics](https://www.cbn.gov.ng/PaymentsSystem/ePaymentStatistics.html)

CBN statistics provide additional aggregate context on digital payment activity in Nigeria. They are not merged with the synthetic dataset or used to calculate transaction-level reliability metrics.

## 5. Findings

An initial data audit was conducted to assess the dataset's structure, completeness, consistency, and suitability for analysis.

### Data Audit Results

| Audit Area | Finding | Analytical Decision |
|---|---|---|
| Dataset structure | 5 million records and 16 original columns | Retain the dataset |
| Missing values | No missing values in audited fields | Retain |
| Duplicate IDs | No duplicate transaction IDs | Retain |
| Date coverage | 730 consecutive calendar days | Retain |
| Transaction amounts | All amounts are positive and multiples of NGN 100 | Document as a synthetic data characteristic |
| Balance fields | Balance movements do not reliably reflect transaction outcomes | Exclude both balance fields |
| Fraud indicator | Approximately 0.8% prevalence with negligible association with transaction status | Descriptive use only |

### Analytical Dataset

Following the data audit, both balance fields were excluded because their movements did not reliably reflect transaction outcomes.

The resulting analytical dataset contains:

- **Records:** 5,000,000
- **Original columns:** 16
- **Excluded columns:** 2 balance fields
- **Final analytical columns:** 14

These decisions help ensure that subsequent analysis focuses on variables relevant to transaction monitoring.

## 6. Scenario-Based Simulation

The project uses three controlled scenarios to evaluate how monitoring indicators respond to changes in transaction outcomes.

All scenario transformations are applied to copies of the baseline dataset. The original dataset remains unchanged.

All simulated results are labelled **Scenario Test Output, Not Observed Data**.

### Scenario A: Peak-Hour Mobile Failure Increase

| Parameter | Definition |
|---|---|
| Channel | Mobile |
| Event period | 17–30 June 2024 |
| Time window | 18:00–19:59 |
| Baseline failure probability | 7% |
| Simulated failure probability | 12% |
| Change | Increase in failed transaction probability |

**Purpose:** Test whether monitoring can identify a sustained increase in failed mobile transactions during a defined peak-hour window.

### Scenario B: Pending and Reversal Increase

| Parameter | Definition |
|---|---|
| Channel | All channels |
| Event date | 15 September 2024 |
| Time window | 12:00–17:59 |
| Pending adjustment | Increase by 3 percentage points |
| Reversal adjustment | Increase by 2 percentage points |
| Failed transactions | Unchanged |

**Purpose:** Test whether monitoring can identify increases in pending and reversed transaction shares while the failure rate remains unchanged.

This scenario demonstrates why monitoring only failed transactions may overlook other important changes in transaction outcomes.

### Scenario C: Telecom Merchant Category Failure Increase

| Parameter | Definition |
|---|---|
| Merchant Category Code | MCC 4814 |
| Event date | 28 June 2023 |
| Time window | 06:00–17:59 |
| Baseline failure rate | Approximately 7.24% |
| Simulated target failure rate | 15% |
| Change | Increase in failed transactions within the selected merchant category |

**Purpose:** Test whether monitoring can identify an increase in transaction failures within a specific merchant category.

The simulation uses the same target population before and after injection. The comparison is a controlled scenario test, not an independent-sample experiment.


## 8. Disclaimer

This project is an educational and analytical demonstration using synthetic transaction data.

The findings do not represent actual Nigerian banking transactions, customer behaviour, payment-system performance, or financial institution reliability.

All simulated results are controlled test outputs and must not be interpreted as observed payment incidents.

The project does not use confidential employer, customer, or production transaction data.

##  Acknowledgement

This project was completed as part of the **SmartBizCrux Python Study Group**.
