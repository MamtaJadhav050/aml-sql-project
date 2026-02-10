# aml-sql-project
SQL-first, rule-based AML transaction monitoring framework with governance and audit-ready design (no ML).

## Overview
This project focuses on building a practical, rule-based Anti-Money Laundering (AML) 
transaction monitoring framework using SQL. The system reviews account-level 
transaction behavior over time to highlight patterns that may warrant further 
review by compliance teams.

The design follows common banking AML practices and avoids machine learning 
models in favor of transparent rules that are easier to explain, audit, and 
maintain in regulated environments.

---

## Business Objective
Banks are required to monitor customer transactions to identify activity that 
could indicate potential money laundering. Given the scale of transaction data 
and regulatory expectations, manual monitoring is not feasible.

The goal of this project is to support compliance teams by:
- Identifying unusual or high-risk transaction behavior at the account level
- Prioritizing cases so investigators can focus on the most relevant alerts
- Providing clear reasoning for why an account was flagged
- Incorporating governance and control considerations expected in regulated settings

---

## Scope

### In Scope
- Account-level transaction monitoring
- Daily aggregation of transactional activity
- Rolling window analysis over 7, 30, and 60 days
- Rule-based AML typologies such as structuring, velocity, and dormant-to-active behavior
- Risk scoring and alert prioritization
- Governance and supporting documentation

### Out of Scope
- Machine learning or predictive models
- Automated filing of Suspicious Activity Reports (SARs)
- Law enforcement or legal decision-making

---

## Technical Approach
- SQL-first analysis using MySQL 8.0+
- Rule-based logic aligned with common AML monitoring practices
- Daily processing pipeline:
  `transactions → daily aggregates → behavioral features → rules → alerts`
- Focus on explainability, traceability, and audit readiness

---

## AML Typologies Covered
The rules in this project are designed around common AML monitoring scenarios, including:
- Structuring through repeated near-threshold cash deposits
- Unusual transaction velocity or bursts of activity
- Dormant accounts that suddenly become active
- Rapid movement of funds in and out of an account (layering proxy)
- High reliance on cash relative to total inflows

---

## Data Model
The monitoring pipeline is built using a small set of core tables:
- `transactions_raw` – Raw transaction data used as the system input
- `account_daily_base` – Daily transaction summaries at the account level
- `account_daily_features` – Rolling behavioral metrics used for monitoring
- `rule_hits` – Results of individual rule evaluations with explanations
- `alerts` – Prioritized list of accounts for compliance review

---

## Governance & Controls
In addition to detection logic, the framework includes governance considerations 
commonly found in AML environments:
- Defined rule lifecycle and review process
- Threshold tuning and alert volume monitoring
- Change management and supporting documentation

These controls help ensure the monitoring framework remains effective, 
manageable, and defensible from a regulatory perspective.
