# SMB Sales & Pipeline Operations Review
### Turning raw CRM opportunity data into clearer sales decisions

**Author:** Yashpal Saini  

---

## Executive Summary

This project analyzes CRM sales opportunity data to understand how a sales organization is performing across teams, products, sectors, and stages of the pipeline. The goal is not just to report numbers, but to answer business questions that leaders care about:

- Which teams are closing the most revenue?
- Which sales agents need support?
- Which products convert best?
- Which sectors are most attractive?
- Where is the pipeline slowing down?

To answer those questions, I built an end-to-end workflow across **Python, SQL, and Power BI**. The project starts with raw CSV files, standardizes them for cleaner analysis, loads them into a relational database, uses SQL to answer business questions, and finishes with an interactive report for decision-makers.

For a non-technical reader, the simplest way to think about this project is:

> **This is a sales operations review.**  
> It helps a business understand what is working in the pipeline, what is not, and where to focus time, training, and commercial effort.

---

## Why This Project Matters

Sales teams often have plenty of raw CRM data but limited clarity on what it actually means. A pipeline can look healthy on the surface while hiding problems such as:

- uneven team performance
- low conversion in specific products or sectors
- long sales cycles
- underperforming reps
- over-reliance on a small number of high-performing accounts

This project turns those raw records into a decision-support system that can help leaders:

- improve pipeline visibility
- compare team performance fairly
- identify bottlenecks
- prioritize higher-value opportunities
- support more informed planning

That business framing is what makes the project relevant to strategy, operations, sales planning, and growth analytics roles.

---

## Business Questions Answered

The analysis is organized around practical sales-operations questions:

### 1) Sales Team Performance
- Which teams generate the most revenue?
- Which teams close the most deals?
- Which teams have the strongest success rate?

### 2) Sales Agent Performance
- Which agents are underperforming on revenue or won opportunities?
- Which agents are above or below their team average?
- Are there agents with no assigned opportunities?

### 3) Quarterly Trends
- How do won deals and revenue change quarter over quarter?
- How do success rates shift over time?

### 4) Product Performance
- Which products have the highest win rates?
- Which products generate the most revenue?
- Which products move through the pipeline faster?

### 5) Market / Sector Performance
- Which industries generate the most revenue?
- Which sectors have the highest success rates?
- Where is the strongest commercial opportunity?

### 6) Sales Cycle Efficiency
- How long does it take to close won vs. lost deals?
- Which products or sectors have longer cycles?
- Where might the pipeline be getting stuck?

---

## Dataset

This project uses a CRM-style B2B sales dataset from **Maven Analytics** focused on a computer hardware company.

### Source Files
- `accounts.csv`
- `sales_teams.csv`
- `products.csv`
- `sales_pipeline.csv`

### Main Entities
- **Accounts:** client companies, sectors, size, location
- **Sales Teams:** agents, managers, regional offices
- **Products:** product names, series, list prices
- **Sales Pipeline:** opportunity stages, dates, values, ownership

---

## Project Workflow

This repository is structured as a complete analytics workflow rather than a single notebook or dashboard.

### 1. Data Preparation
The raw files are reviewed and cleaned in Python.

Key work completed:
- examined each source file
- added integer IDs for agents, products, and accounts
- created mapping logic to replace full names with IDs
- validated consistency across source files
- corrected mismatched or misspelled values
- saved cleaned files for database loading

**Why this matters:**  
This step improves data consistency and makes joins faster and safer.

### 2. Data Modeling
The cleaned files are loaded into a relational database.

Database design includes:
- `sales_teams` dimension table
- `products` dimension table
- `accounts` dimension table
- `sales_pipeline` fact table

The model supports:
- easier joins
- better query performance
- clearer separation between reference data and transactional pipeline data

### 3. Data Analysis
The core business analysis is done in SQL.

Techniques used include:
- joins
- aggregations
- Common Table Expressions (CTEs)
- window functions
- ranking logic
- quarter-over-quarter trend calculations
- success-rate formulas
- sales cycle calculations

### 4. Report Creation
The final output is an interactive Power BI report designed for business users.

The report provides:
- KPI summaries
- trend views
- product and sector analysis
- sales team and agent comparisons
- drilldowns by quarter

---

## Key Insights

Below are a few example findings surfaced in the analysis.

### Sales Teams
- Six distinct sales teams are analyzed using the combination of **regional office + manager**.
- The **Central team managed by Melvin Marxen** generated the highest won revenue at **2,251,930** across **882 won opportunities**.
- The **East team managed by Cara Losch** recorded the highest success rate at **64.43%**, showing that the most efficient team is not always the team with the most revenue.

### Sales Agents
- Some agents had **no recorded opportunities**, which may indicate onboarding, reassignment, or data-quality issues.
- The lowest-performing agents by revenue were not always the same as the lowest-performing agents by won deals, which is important for performance review and coaching.

### Pipeline Trends
- Quarter-over-quarter analysis helps show whether revenue changes are driven by volume, close rates, or both.
- This helps separate a pipeline coverage problem from a conversion-efficiency problem.

### Products and Sectors
- Product win rates and revenue contribution vary significantly.
- Sector analysis shows where the company both wins more often and generates stronger revenue, which can support targeting and account prioritization.

### Sales Cycle
- Won and lost deals have different average cycle lengths.
- Comparing cycle time by product and sector helps identify where the sales process is slowest.

---

## Business Recommendations

Based on this type of analysis, a sales or strategy team could take actions such as:

- review low-performing reps relative to their team average
- investigate why some agents have no assigned opportunities
- prioritize products with stronger win rates and faster cycle times
- focus sector outreach on higher-conversion industries
- improve planning in teams with high volume but lower success rates
- monitor quarter-over-quarter changes to catch pipeline deterioration early

These recommendations are intentionally practical. The project is designed to support decisions, not just dashboards.

---

## Tech Stack

- **Python** – data cleaning and transformation
- **SQL (MySQL-style workflow)** – analysis, modeling, KPI logic
- **Power BI** – interactive reporting and business-facing dashboards
- **Jupyter Notebook** – preparation workflow
- **CSV files** – source data

---

## Repository Structure

```text
CRM_Sales_Opportunities_project-main/
├── 1. Data Preparation/
│   ├── csv_files_preparation.ipynb
│   ├── original_files/
│   ├── modified_files/
│   └── README.md
├── 2. Data Modelling/
│   ├── db_creation_crm_sales.sql
│   ├── db_crm_sales_diagram.png
│   └── README.md
├── 3. Data Analysis/
│   ├── db_analysis.sql
│   └── README.md
├── 4. Report Creation/
│   ├── CRM_sales_report.pbix
│   ├── CRM_sales_report.pdf
│   └── README.md
└── README.md
```

---

## How to Reproduce the Project

### Option 1: Review the project outputs
If you want to understand the work quickly:
1. open the SQL analysis file
2. review the Power BI report PDF
3. explore the report logic by folder

### Option 2: Rebuild the workflow end to end
1. Review the raw CSV files in `1. Data Preparation/original_files`
2. Run the Jupyter notebook in `1. Data Preparation/csv_files_preparation.ipynb`
3. Create the database using `2. Data Modelling/db_creation_crm_sales.sql`
4. Load the cleaned CSV files into the database
5. Run the SQL analysis in `3. Data Analysis/db_analysis.sql`
6. Open the Power BI file in `4. Report Creation/CRM_sales_report.pbix`

---

## What This Project Demonstrates

This project demonstrates the ability to:

- translate raw CRM data into business-ready analysis
- build a structured analytical workflow from data prep to reporting
- use SQL to answer commercial performance questions
- compare team, agent, product, and sector performance
- communicate findings in a format useful to leaders and non-technical stakeholders

For hiring managers, this project is best understood as a **sales operations and decision-support case study**, not just a dashboard exercise.

---

## Recruiter-Friendly Project Summary

**SMB Sales & Pipeline Operations Review**  
Built an end-to-end sales operations analysis using Python, SQL, and Power BI to evaluate pipeline performance across teams, agents, products, and sectors. Standardized CRM data for relational modeling, used SQL to diagnose performance gaps and sales-cycle bottlenecks, and created a business-facing report to support pipeline visibility, prioritization, and planning decisions.

---

## Suggested Resume Bullets

- Built an end-to-end sales pipeline analysis in Python, SQL, and Power BI to evaluate revenue performance, win rates, and sales-cycle trends across teams, products, and sectors.
- Standardized CRM opportunity data for relational analysis, then used SQL with CTEs and window functions to identify underperforming reps, product-level conversion patterns, and quarter-over-quarter pipeline shifts.
- Created a business-facing Power BI report that translated pipeline data into actionable recommendations on team performance, sector focus, and commercial prioritization.

---

## Notes

- The dataset represents a fictitious company and is used for analytical practice and business case development.
- Some intermediate-stage deals do not have assigned accounts, which affects certain market-level analyses.
- The project intentionally balances technical rigor with business interpretation so that both analysts and non-technical stakeholders can use the outputs.

---

## Author

**Yashpal Saini**
