# Veritas Bank — Customer Churn & Retention Analytics
A comprehensive customer churn and retention intelligence solution built for Veritas Bank, transforming customer account data into an interactive, multi-view Power BI analytics report. This project replaces intuition-based retention strategies with a data-driven single source of truth for bank leadership, enabling proactive churn mitigation across the UK, Germany, and France. 

## Table of Contents
- [Overview](#overview)
- [Project Brief and Problem Statement](#Project-Brief-and-Problem-Statement)
- [Data Pipeline and Architecture](#Data-Pipeline-and-Architecture)
- [Data Transformation and Cleaning](#Data-Transformation-and-Cleaning)
- [Data Model and Relationships](#Data-Model-and-Relationships)
- [Core DAX Measures and Formulas](#Core-DAX-Measures-and-Formulas)
- [Dashboards and Visualizations](#Dashboards-and-Visualizations)
- [Key Business Insights](#Key-Business-Insights)
- [Strategic Recommendations](#Strategic-Recommendations)
- [Tech Stack](#Tech-Stack)
- Author

## Overview
Veritas Bank is a UK-headquartered retail bank established in the 1990s with major operations across Germany and France, serving over 3 million customers. Despite its strong digital presence, the bank faced rising customer churn due to intense fintech competition and lower engagement in continental markets. 

This project establishes a business intelligence framework by structuring customer account transaction files into a relational data model, applying ETL transformations, and creating intuitive visuals that allow leadership to track churn drivers, and customer demographics. 

## Project Brief and Problem Statement
### Problem Statement 
Veritas Bank lacked real-time churn monitoring and behavioral segmentation. Decisions were traditionally made reactively without granular insights into why customers leave, making it difficult to optimize acquisition, evaluate credit health, and prevent revenue loss across European markets. 

### Project Objectives
- Centralize Retention Visibility: Track overall customer churn rates, active account ratios, and total regional balances. 
- Demographic & Regional Intelligence: Evaluate churn behavior and account usage across the UK, Germany, and France. 
- Targeted Risk Mitigation: Segment high-risk customer profiles (e.g., by age group, activity status, or product density) to guide marketing and retention policies. 
  
## Data Pipeline and Architecture
[Raw Dataset] ➔ [Data Prep & Feature Engineering] ➔ [Data Model] ➔ [Interactive Power BI Report]

## Data Transformation and Cleaning
### ETL & Data Transformation Steps 
- Data Hygiene & Quality Checks: Cleaned null values, validated unique CustomerId records, and verified column data type. 
- Feature Engineering: Derived structural grouping attributes including Age Group bins (e.g., 10–19, 20–29, 30–39) and Balance Group tiers (e.g., 0, 1–19.9K, 20K–39.9K).  

## Data Model and Relationships
The data model connects dim_customer table with fact_accounts table via a 1:1 relationship linked on CustomerId.

<img width="1011" height="499" alt="VB Data Model" src="https://github.com/user-attachments/assets/e750bfd0-73b9-4e8a-bccc-0205042623c2" />

dim_customer: Lookup table containing customer demographic attributes (CustomerId, Country, Age, Age (bins), Age Group).
fact_accounts: Fact/Operational table containing financial and activity attributes (CustomerId, CreditScore, Balance, Balance Group, CreditCard, ActiveMember).

## Core DAX Measures and Formulas
- Total Customers = COUNT(CustomerInfo[CustomerId])
- Total Churned = CALCULATE(COUNT(AccountInfo[CustomerId]), AccountInfo[Exited]=1)
- Churn Rate = DIVIDE(CALCULATE(COUNTROWS(AccountInfo),AccountInfo[Exited] = "1"), COUNTROWS(AccountInfo))


## Dashboards and Visualizations
### Dashboard 1 — Customer Demographics
Provides executive visibility into total customer counts, overall churn metrics, regional balance totals, and demographic distributions.

<img width="600" height="448" alt="Demographics" src="https://github.com/user-attachments/assets/973804fd-ea5e-4fbb-a939-0da48616de04" />

- KPI Header: Total Customers (10K), Churn Rate (13.85%), Avg. Credit Score (651), UK Balance (£138.1M), and Europe Balance (€133.47M).
- Demographic Distributions: Donut chart for Customers by Country (UK 5.01K, Germany 2.51K, France 2.48K) and bar charts for Age groups (led by 30–39 at 3.38K and 40–49 at 3.23K) and Gender (5.7K Male / 4.3K Female).
- Account Characteristics: Column chart breakdowns displaying Active Status (5.2K Active / 4.8K Inactive), Number of Products (4.8K hold 1 product, 4.7K hold 2), and Credit Card Ownership (7.2K Cardholders / 2.8K Non-Cardholders).

### Dashboard 2 — Churn Analysis
Isolates specific churn volumes across demographics, product density, account activity, and balance tiers to highlight attrition risk factors.

<img width="598" height="447" alt="Churn 1" src="https://github.com/user-attachments/assets/e9a09a46-00b0-47f2-924a-d43aaa8a8f88" />

<img width="599" height="448" alt="Churn 2" src="https://github.com/user-attachments/assets/ad30ad57-fdf0-44c4-a6e2-1562239a768e" />

- Demographic Churn Drivers: Churn count ranked by Country (UK 498, Germany 453, France 434), Age Group (led by 30–39 with 490 churned and 40–49 with 450 churned), and Gender (767 Male / 618 Female).
- Financial Risk Factors: Churn volume concentrated in zero balance accounts (829 churned) compared to funded tiers.
- Operational Risk Factors: Churn metrics broken down by Number of Products (670 churned with 1 product, 654 with 2 products), Tenure (540 churned at 3–5 years tenure).


## Key Business Insights
### Financial & Demographic Intelligence
- Customer Base & Churn Baseline: Veritas Bank serves 10,000 customers across three markets with an overall churn rate of 13.85% (1,385 total churned customers) and an average credit score of 651.
- Regional Disparity: The UK holds 50.1% of the customer base (5.01K) and £138.1M in total balance, whereas Germany and France account for approximately 2.5K customers each with €133.47M in combined European balances.
- Age Vulnerability: Customers aged 30–49 represent the largest segment (6.61K customers) and account for the vast majority of overall churn (940 total churned customers).

### Operational Risk Insights
- Inactivity Risk: Inactive status is the single highest predictor of churn — 1,385 inactive members churned while active members exhibited zero churn in the dataset.
- Additionally, churn is highest among single-product holders (670 churned) and 2-product holders (654 churned).
- Zero-Balance Depletion: Customers holding a zero-balance account account for 829 churned cases (60% of total churn), signaling account abandonment prior to formal exit.

## Strategic Recommendations
- Targeted Inactivity Re-Engagement: Implement automated re-engagement campaigns (e.g., fee waivers, promotional interest rates) targeting inactive accounts at the 3-year tenure mark.
- Tailored Loyalty Programs for 30–49 Age Group: Develop specialized rewards (e.g., mortgage discounts, premium wealth management) tailored to core middle-aged demographics in Germany and France.
- Early Warning Indicator System: Deploy real-time alerting when a customer's balance drops to zero or activity flags as inactive.

## Tech Stack
- Data Transformation & Modeling: PowerQuery, DAX
- Visualization: Microsoft PowerBI
