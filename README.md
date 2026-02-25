# Finance-Analytics-Dashboard
### End-to-End Business Intelligence Solution | Power BI

---

> **Project Summary:** Designed and deployed an interactive Personal Finance Dashboard in Power BI to consolidate multi-year income, expense, and savings data — transforming fragmented financial records into a single source of truth that enables real-time performance monitoring and data-driven financial decisions.

---
## Dashboard Preview 

<img width="1443" height="818" alt="image" src="https://github.com/user-attachments/assets/5b1207be-53c0-4b3e-8e45-919ccf17db36" />

---

## Executive Summary

Most individuals manage their finances through fragmented spreadsheets or siloed banking apps — resulting in delayed awareness of spending patterns, no visibility into savings efficiency, and reactive rather than proactive financial management.

This project builds a **centralized, interactive Personal Finance Dashboard** using Microsoft Power BI that consolidates 4+ years of financial data (2021–2024) across income, savings, and expense categories. The solution enables:

- Real-time monitoring of income, expenses, and savings across ₹2.79M+ in tracked financial activity
- Identification of spending inefficiencies and savings growth drivers
- Self-service financial analytics with interactive slicers and drill-down capability

**Key outcome:** Total savings of ₹539.7K achieved in 2023 alone on ₹964.2K income — a **56% savings rate** — surfaced and validated through automated dashboard reporting.

---

## Business Problem

### Current State
Personal finance management is plagued by fragmentation:
- Data scattered across bank statements, Excel sheets, and UPI apps
- Manual month-end reconciliation is time-consuming and error-prone
- No unified view of financial health across time and category
- Limited ability to identify which spending categories are eroding savings

### Key Pain Points

| Pain Point | Impact |
|---|---|
| No consolidated financial view | Blind spots in spending and savings trends |
| Manual reporting | 2–4 hours/month in reconciliation effort |
| Lagging indicators | Insights available only after the damage is done |
| No trend visibility | Cannot identify seasonal patterns or savings decay |

---

## Project Objectives

This dashboard was built to:

1. **Unify** income, expense, and savings data into a single interactive interface
2. **Track** core financial KPIs: Income Growth, Savings Rate, Expense Ratio, and Month-over-Month changes
3. **Enable** multi-dimensional analysis across time (monthly/yearly), category (EMIs, Groceries, Health), and savings vehicle (Liquid Cash, Mutual Funds, Fixed Deposits)
4. **Surface** actionable insights on spending inefficiencies and savings optimization opportunities

---

## Dataset & Scope

### Data Coverage
| Dimension | Details |
|---|---|
| **Time Range** | 2021 – 2024 (4 years) |
| **Total Financial Activity** | ₹2.79M tracked |
| **Income Sources** | Salary, Freelancing |
| **Expense Categories** | House Rent, EMIs, Groceries & Food, Health, Shopping, Leisure, Other |
| **Savings Vehicles** | Liquid Cash, Mutual Funds, Fixed Deposits, Emergency Fund |

### 2023 Snapshot (Primary Analysis Year)
| Category | Amount |
|---|---|
| Total Income | ₹964,200 |
| — Salary | ₹901,200 |
| — Freelancing | ₹63,000 |
| Total Expenses | ₹514,090 |
| — EMIs | ₹124,000 |
| — Groceries & Food | ₹112,000 |
| Total Savings | ₹539,700 |
| — Liquid Cash | ₹433,500 |
| — Mutual Funds | ₹86,000 |

---

## Methodology

The project follows a structured **6-stage BI pipeline**:

```
Raw Data → Ingestion → Cleaning → Modeling → KPI Development → Visualization → Deployment
```

### Stage 1: Data Ingestion
- Imported multi-year financial data from structured CSV/Excel sources into Power BI Desktop
- Consolidated income, expense, and savings tables into a unified data environment

### Stage 2: Data Cleaning (Power Query)
- Removed null and duplicate entries across all tables
- Standardized date formats; created derived `Year` and `Month` columns for time intelligence
- Normalized category labels for consistent aggregation across years

### Stage 3: Data Modeling
- Designed a **Star Schema** architecture linking a central fact table to date and category dimensions
- Established correct table relationships to enable accurate cross-filtering

### Stage 4: KPI Development (DAX)
- Created core and advanced measures including MoM growth, savings rate, expense ratio, and YTD totals
- Built dynamic KPI cards responding to slicer selections

### Stage 5: Dashboard Design
- Designed a clean, executive-facing layout with KPI cards, trend lines, and donut charts
- Applied consistent color coding (income = purple, savings = teal, expenses = contrast)

### Stage 6: Deployment
- Published dashboard to Power BI Service for ongoing access and refresh

---

## Data Model Architecture

The model follows a **Star Schema** design optimized for performance and analytical flexibility:

```
          ┌─────────────┐
          │  Dim: Date  │
          └──────┬──────┘
                 │
┌──────────┐    │    ┌────────────────┐
│Dim:      ├────┼────┤  Fact: Finance │
│Category  │    │    │  Transactions  │
└──────────┘    │    └────────────────┘
                │
          ┌─────┴──────┐
          │ Dim: Type  │
          │(Inc/Exp/Sav│
          └────────────┘
```

**Fact Table:** Financial Transactions (Date, Amount, Type, Category, SubCategory)

**Dimension Tables:** Date, Category, Type (Income / Expense / Savings)

---

## KPI Framework & DAX Measures

### Core KPIs Tracked

| KPI | Definition | 2023 Value |
|---|---|---|
| Total Income | Sum of all income sources | ₹964,200 |
| Total Expenses | Sum of all spending | ₹514,090 |
| Total Savings | Net income minus expenses | ₹539,700 |
| Savings Rate | Savings ÷ Income | 56% |
| Expense Ratio | Expenses ÷ Income | 53% |
| Exp vs Savings % | Expense ÷ Savings ratio | 140% |

### Sample DAX Measures

```dax
-- Core Aggregations
Total Income    = CALCULATE(SUM(Finance[Amount]), Finance[Type] = "Income")
Total Expense   = CALCULATE(SUM(Finance[Amount]), Finance[Type] = "Expense")
Total Savings   = CALCULATE(SUM(Finance[Amount]), Finance[Type] = "Savings")

-- Rate Calculations
Savings Rate    = DIVIDE([Total Savings], [Total Income], 0)
Expense Ratio   = DIVIDE([Total Expense], [Total Income], 0)

-- Month-over-Month Growth
MoM Income Growth =
  VAR CurrentMonth = [Total Income]
  VAR PrevMonth    = CALCULATE([Total Income], DATEADD('Date'[Date], -1, MONTH))
  RETURN DIVIDE(CurrentMonth - PrevMonth, PrevMonth, 0)

-- Year-to-Date
YTD Savings     = TOTALYTD([Total Savings], 'Date'[Date])
```

---

## Dashboard Design

The dashboard is structured as a **single-page executive view** with four analytical zones:

### Zone 1 — KPI Cards (Top Right)
Displays Income, Expense %, Savings %, and Total Savings with month-over-month change indicators (▲/▼ arrows + percentage deltas).

### Zone 2 — Trend Line Chart (Top Left)
`Expenses by Date` line chart tracking the expense-to-income ratio across 2023 (Jan–Dec), revealing a mid-year trough (July minimum ~49%) and late-year spike — flagging Q4 as a high-spend period.

### Zone 3 — Composition Charts (Bottom Center)
- **Spendings donut chart** — visual breakdown of ₹514.09K across House Rent, EMIs, Groceries, Health, Shopping, Leisure, Other
- **Savings donut chart** — visual breakdown of ₹539.7K across Liquid Cash (80%), Mutual Funds (16%), Fixed Deposits, Emergency Fund

### Zone 4 — Detail Table (Bottom Right)
Hierarchical income statement-style table showing exact figures by Type > SubCategory for any selected year.

### Interactive Filters
- Year selector (2021 / 2022 / 2023 / 2024 / Select All)
- Month dropdown (e.g., Jul-23)

---

## Key Insights Generated

**1. Savings Rate Exceeds Benchmark**
A 56% savings rate in 2023 significantly outperforms the 20–30% personal finance benchmark — driven primarily by controlled grocery (₹112K) and health (₹37K) spending relative to income.

**2. Salary is the Dominant Income Driver — Freelancing is Untapped**
Freelancing contributes only ₹63,000 (6.5% of total income). Even a 2x growth in freelance revenue would add ~₹63K to savings with minimal incremental expense.

**3. EMIs are the Largest Expense Block**
EMIs at ₹124,000 represent 24% of total expenses — the single largest category. Any EMI prepayment or refinancing could meaningfully improve the savings rate in future years.

**4. Savings Portfolio is Overly Concentrated in Liquid Cash**
₹433,500 (80%) of savings sits in liquid cash — generating low to minimal returns. Rebalancing 30–40% into mutual funds or fixed deposits could improve overall portfolio yield.

**5. Expense Volatility Peaks in Q4**
The trend line shows expense ratio climbing from ~49% in July to ~55%+ by Q4. This seasonal pattern suggests budget planning for year-end spending (shopping, leisure, health) could improve savings consistency.

**6. Multi-Year Context (2021–2024): ₹2.79M Total Activity**
Across all tracked years, total financial activity reached ₹2.79M with ₹1.79M in cumulative net worth generated — a strong indicator of consistent savings discipline over time.

---

## Business Impact

| Impact Area | Outcome |
|---|---|
| **Reporting Efficiency** | Eliminated manual monthly reconciliation (~3 hrs/month) |
| **Decision Speed** | Real-time KPI access vs. end-of-month awareness |
| **Financial Visibility** | Single view across 4 years, 3 categories, 10+ sub-categories |
| **Savings Optimization** | Identified ₹433K liquid cash rebalancing opportunity |
| **Pattern Recognition** | Surfaced Q4 expense spike enabling proactive budgeting |

---

## Challenges & Solutions

| Challenge | Approach |
|---|---|
| Inconsistent category labels across years | Power Query normalization and lookup tables |
| Designing MoM calculations across year boundaries | DATEADD-based DAX time intelligence functions |
| Avoiding visual clutter in single-page layout | Zone-based layout with KPI cards, charts, and table in distinct areas |
| Ensuring cross-filter accuracy | Proper star schema relationships with single-direction filters |

---

## How to Run

```
1. Clone or download the repository
2. Open Finance_Dashboard.pbix in Power BI Desktop
3. If prompted, update the data source path to your local CSV file
4. Click "Refresh" to load the latest data
5. Use the Year and Month slicers to explore insights interactively
```
