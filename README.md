Credit Contract Portfolio & Risk Analytics

A Power BI credit analytics project covering portfolio growth, disbursement KPI performance, repayment efficiency, overdue exposure, concentration risk, maturity pressure, and contract-level monitoring.

Dashboard Preview

01. Credit Portfolio Overview



02. Disbursement KPI



03. Repayment & Collection Efficiency



04. Portfolio Quality & Risk



Note: The Power BI dashboard interface is presented in Vietnamese because the project was developed for a Vietnamese banking business context. This README is written in English for portfolio presentation.

Project Overview

This project analyzes the full credit contract lifecycle in a banking environment, from disbursement and outstanding balance to repayment performance, overdue exposure, and portfolio risk.

The reporting flow is structured into four analytical layers:

Credit Portfolio Overview
→ Disbursement KPI
→ Repayment & Collection Efficiency
→ Portfolio Quality & Risk

The goal is not only to describe the portfolio, but also to identify where business performance is below plan, where overdue exposure is concentrated, and which branches or contracts require management attention.

Project Information

Item

Description

Project Name

Credit Contract Portfolio & Risk Analytics

Domain

Banking / Credit Analytics

Role

Data Analyst

Tools

Power BI, DAX, SQL Server, Excel

Reporting Period

2024 Q4

Latest Data Date

27/12/2024

Status

Completed

Dashboard Language

Vietnamese

Business Context

Credit portfolio management requires more than monitoring total loan disbursement.

Management also needs to understand:

how the outstanding portfolio changes over time;

whether branches are meeting disbursement targets;

whether scheduled principal and interest are being collected;

how much principal remains overdue;

how overdue exposure is distributed by aging bucket;

where portfolio concentration exists by branch, customer, and industry;

which contracts are approaching maturity;

which contracts or branches should be prioritized for monitoring.

This project combines these perspectives into a single Power BI solution to support performance monitoring and risk-oriented decision-making.

Business Questions

This project focuses on the following questions:

How much credit was disbursed during the reporting period?

How did outstanding principal change from the beginning to the end of the period?

Which regions, terms, and branches hold the largest outstanding balances?

How does actual disbursement compare with quarterly branch targets?

Which branches contribute most to the KPI shortfall?

How much principal and interest should have been collected?

What percentage of scheduled principal and interest was actually recovered?

How much principal remains overdue?

How long has overdue principal remained unpaid?

Which branches contribute most to total overdue principal?

How concentrated is credit exposure by customer and industry?

How much outstanding balance will mature in the near term?

Is portfolio growth accompanied by higher overdue risk?

Which contracts should be placed on a monitoring watchlist?

Dataset Overview

The Power BI model combines credit-contract data, repayment schedules, actual repayment transactions, customer and branch dimensions, disbursement plans, industry classifications, collateral information, and analytical helper tables.

Main Tables

Table

Purpose

HOPDONG_TINDUNG

Credit contract information such as contract ID, customer, disbursement date, maturity date, amount, term, and interest rate

KE_HOACH_TRA_NO

Scheduled repayment obligations by contract and repayment period

KHACHHANG_TRANO

Actual principal and interest repayment transactions

KEHOACH_GIAINGAN

Branch-level disbursement plans

KHACHHANG

Customer master data

CHINHANH

Branch master data

KHUVUC

Regional classification

DateTable

Main date dimension

NGANHNGHE_KINHTE_CAP01/02/03

Industry classification hierarchy

TAISAN_BAODAM

Collateral information

Dim_Thoigian_KPI

Reporting-period helper table

Dim_Aging

Overdue aging buckets

Forecast_Bridge

Disconnected table used for KPI forecast waterfall

Raw data is not included in this repository. The dataset is used for academic and portfolio purposes.

Data Modeling Approach

The credit contract is the central analytical entity.

A simplified model is:

                    CHINHANH
                        |
                        |
KHACHHANG ------ HOPDONG_TINDUNG
                        |
                -------------------
                |                 |
                v                 v
       KE_HOACH_TRA_NO     KHACHHANG_TRANO
       Repayment Plan      Actual Repayment

The project uses several different date roles:

Date Field

Business Meaning

HOPDONG_TINDUNG[NGAY_GIAINGAN]

Credit disbursement date

KE_HOACH_TRA_NO[NGAY_CUOIKY]

Scheduled repayment due date

KHACHHANG_TRANO[NGAYTRA]

Actual repayment date

HOPDONG_TINDUNG[NGAY_DAOHAN]

Contract maturity date

To handle these date roles correctly, the model uses DAX techniques including:

CALCULATE

FILTER

REMOVEFILTERS

USERELATIONSHIP

CROSSFILTER

TREATAS

SUMX

RANKX

TOPN

ALLSELECTED

Reporting Date Logic

Historical analysis is evaluated using an as-of reporting date.

Conceptually:

Reporting Date =
MIN(
    Selected KPI Period End Date,
    Latest Available Data Date
)

This prevents future transactions from affecting historical reporting periods.

Example:

Selected Period: 2020 Q4
Period End:      31/12/2020
Latest Data:     27/12/2024

Effective Reporting Date = 31/12/2020

For the latest period:

Selected Period: 2024 Q4
Period End:      31/12/2024
Latest Data:     27/12/2024

Effective Reporting Date = 27/12/2024

Dashboard 01 – Credit Portfolio Overview

Objective

Provide a management-level view of portfolio size, portfolio growth, credit structure, disbursement, repayment, and branch exposure.

Key KPIs

KPI

2024 Q4

Contracts Disbursed

426

Total Disbursement

396.53B VND

Beginning Outstanding Principal

3.23T VND

Ending Outstanding Principal

3.45T VND

Principal Collected During Period

180.16B VND

Interest Collected During Period

67.72B VND

Cumulative Principal Collected

1.56T VND

Cumulative Interest Collected

946.96B VND

Portfolio Growth

~6.69%

Key Insights

The credit portfolio expanded during Q4, with ending outstanding principal increasing from approximately 3.23T VND to 3.45T VND.

The portfolio growth rate was approximately 6.69%, indicating that new disbursement exceeded principal recovery during the period.

426 contracts generated approximately 396.53B VND of new disbursement.

Principal collection reached approximately 180.16B VND, while interest collection reached approximately 67.72B VND.

Exposure is not evenly distributed across branches, making branch-level concentration important for later risk analysis.

The portfolio structure by region and loan term provides the baseline for understanding concentration and maturity pressure.

Management Interpretation

The portfolio continued to grow, but growth alone does not indicate whether business performance is healthy. The next step is to compare actual disbursement with the planned target and identify which branches are driving the gap.

Dashboard 02 – Disbursement KPI

Objective

Measure actual disbursement against quarterly plans and identify branches that require performance intervention.

Key KPIs

KPI

2024 Q4

Planned Disbursement

2.15T VND

Actual Disbursement

396.53B VND

KPI Completion Rate

18.48%

KPI Variance

-1.75T VND

Forecast End-of-Period Disbursement

476.80B VND

Forecast Shortfall

1.67T VND

Required Daily Disbursement Rate

4.74B VND/day

Branches Below KPI

31

Key Insights

Actual disbursement reached only 18.48% of the quarterly plan, showing substantial underperformance against target.

The absolute KPI gap was approximately 1.75T VND.

The forecast of approximately 476.80B VND remained far below the 2.15T VND plan, meaning the portfolio was unlikely to close the gap under the current run rate.

31 branches were still below KPI, showing that the shortfall was broad but not necessarily evenly distributed.

The branch performance scatter plot helps identify the most important management segment: branches with large plans but low completion rates.

Pareto analysis shows which branches contribute most to the total KPI shortfall, allowing management to prioritize a smaller number of high-impact branches.

Some branches can exceed 100% of plan even while the overall system remains far below target, because branch performance is heterogeneous.

Management Interpretation

The main issue is not simply low system-wide performance. The more actionable insight is that resources should be directed toward branches with large planned volumes and large remaining gaps, rather than distributing intervention equally across all branches.

Dashboard 03 – Repayment & Collection Efficiency

Objective

Compare scheduled repayment obligations with actual principal and interest collection, then identify overdue exposure and collection concentration.

Key KPIs

KPI

2024 Q4

Principal Due

1.50T VND

Interest Due

881.48B VND

Principal Collected

1.49T VND

Interest Collected

876.88B VND

Principal Collection Rate

99.31%

Interest Collection Rate

99.48%

Overdue Principal

10.39B VND

Overdue Contracts

19

Key Insights

Overall repayment performance was very strong, with both principal and interest collection rates above 99%.

Despite the strong portfolio-wide collection rate, approximately 10.39B VND of principal remained overdue.

There were 19 overdue contracts, indicating that the remaining collection problem is concentrated in a relatively small number of contracts.

The high collection rate should therefore not be interpreted as “no risk”; it hides a smaller but persistent overdue tail.

Overdue Aging

Aging Bucket

Overdue Principal

>90 days

~5.98B VND

1–30 days

~1.56B VND

31–60 days

~1.53B VND

61–90 days

~1.33B VND

Aging Insights

The >90-day bucket is the largest, representing more than half of total overdue principal.

This indicates that a significant share of overdue exposure is not newly delinquent, but has remained unresolved for an extended period.

Newly overdue balances in the 1–30 day bucket should be addressed early to prevent migration into more severe aging groups.

The aging structure supports a segmented collection strategy instead of treating all overdue exposure equally.

Branch Pareto Insight

Overdue principal is concentrated in a relatively small number of branches.

The cumulative Pareto line shows how many top branches account for the majority of total overdue principal.

This enables collection resources to be concentrated where they can have the greatest portfolio impact.

Management Interpretation

Collection efficiency is excellent at the aggregate level, but the remaining overdue exposure is concentrated and aged. The correct management response is therefore targeted collection, especially for >90-day overdue balances and the branches contributing most to overdue principal.

Dashboard 04 – Portfolio Quality & Risk

Objective

Evaluate portfolio risk exposure, concentration, maturity pressure, branch risk, and contract-level monitoring needs.

Key KPIs

KPI

2024 Q4

Total Outstanding Balance

2.07T VND

Overdue Principal

10.39B VND

Outstanding Balance of Overdue Contracts

45.44B VND

Overdue Contract Exposure Ratio

2.20%

Overdue Contracts

19

Top 10 Customer Concentration

26.37%

Top 3 Industry Concentration

47.08%

Outstanding Balance Maturing ≤30 Days

318.33M VND

The portfolio overview page and the risk page use different analytical measures and scopes for outstanding balance. The risk page focuses on as-of risk exposure and contract-level risk logic.

Key Insights

1. Overdue Exposure Is Limited but Material

Outstanding balance linked to overdue contracts was approximately 45.44B VND.

This represented approximately 2.20% of the risk-analysis outstanding portfolio.

The ratio is not large at portfolio level, but the concentration and aging of the exposure are more important than the headline percentage alone.

2. Customer Concentration

The Top 10 customers account for approximately 26.37% of total outstanding exposure.

This means roughly one quarter of the portfolio is concentrated in only ten customers.

Large-borrower monitoring is therefore important even when aggregate overdue ratios remain low.

3. Industry Concentration

The Top 3 industries account for approximately 47.08% of the portfolio.

Nearly half of total exposure is concentrated in only three industry groups.

This creates sector concentration risk: deterioration in one major industry could have a disproportionate impact on portfolio quality.

4. Maturity Pressure

Only approximately 318.33M VND of outstanding balance is scheduled to mature within the next 30 days.

Most of the portfolio is concentrated in longer maturity buckets, especially contracts with more than 365 days remaining.

Near-term maturity pressure is therefore relatively limited compared with the total portfolio size.

5. Branch Risk Matrix

The branch risk matrix combines:

X-axis      → Outstanding Balance
Y-axis      → Overdue Exposure Ratio
Bubble Size → Overdue Principal

Key interpretation:

Branches in the upper-right area require the highest attention because they combine large portfolio exposure with high overdue ratios.

A branch with a high overdue ratio but small exposure represents a different management priority from a branch with both high exposure and high risk.

This visual helps management distinguish risk severity from portfolio materiality.

6. Portfolio Risk Trend

The trend visual compares:

outstanding balance over time;

overdue-contract exposure ratio over time.

This answers an important portfolio question:

Is credit growth being accompanied by deterioration in credit quality?

Possible interpretations:

Outstanding balance ↑ + Risk ratio ↑ → growth is accompanied by worsening portfolio quality.

Outstanding balance ↑ + Risk ratio ↓ → growth is relatively healthy.

Outstanding balance ↓ + Risk ratio ↑ → potentially concerning because problematic exposure is becoming a larger share of a shrinking portfolio.

Outstanding balance ↓ + Risk ratio ↓ → may indicate successful deleveraging or debt recovery.

7. High-Risk Contract Watchlist

The watchlist moves the dashboard from portfolio-level analysis to actionable monitoring.

It allows management to identify contracts with:

high outstanding exposure;

overdue obligations;

elevated days past due;

approaching maturity;

higher analytical risk priority.

Management Interpretation

The overall overdue exposure ratio remains relatively low, but risk is concentrated by customer, industry, branch, and aging profile. Portfolio management should therefore focus on concentration control and targeted monitoring, not only the aggregate overdue ratio.

Most Important Portfolio Insights

The main findings from the four dashboard pages can be summarized as follows:

1. The Portfolio Is Growing

Outstanding principal increased during Q4, with approximately 396.53B VND of new disbursement across 426 contracts.

2. Growth Is Well Below the Business Plan

Actual disbursement achieved only 18.48% of the quarterly target, leaving a very large KPI gap.

3. Forecast Performance Remains Weak

The forecast remained significantly below target, indicating that current execution speed was insufficient to close the planned disbursement gap.

4. Repayment Performance Is Strong at Aggregate Level

Principal and interest collection rates both exceeded 99%.

5. Aggregate Collection Performance Hides Tail Risk

Despite high recovery rates, 10.39B VND remained overdue across 19 contracts.

6. Overdue Exposure Is Aged

The >90-day overdue bucket was the largest, meaning a substantial portion of overdue principal represents persistent rather than newly emerging delinquency.

7. Overdue Risk Is Concentrated by Branch

Pareto analysis indicates that a limited number of branches contribute a large share of total overdue principal.

8. Customer Concentration Is Material

The Top 10 customers represent 26.37% of portfolio exposure.

9. Industry Concentration Is Higher

The Top 3 industries represent 47.08% of portfolio exposure, making sector concentration one of the most important structural risk findings.

10. Near-Term Maturity Pressure Is Limited

Only approximately 318.33M VND is due to mature within 30 days, while most exposure remains in longer maturity buckets.

Business Recommendations

Based on the findings:

Prioritize branches with large KPI gaps
Focus commercial intervention on branches with large plans, low completion rates, and high forecast shortfalls.

Use Pareto-based management
Allocate collection and performance resources to the small number of branches contributing most to KPI shortfall and overdue exposure.

Prioritize >90-day overdue balances
Long-aged overdue balances should receive the highest collection attention.

Monitor large borrower concentration
The Top 10 customer concentration of 26.37% warrants borrower-level exposure monitoring.

Control industry concentration
With 47.08% of exposure concentrated in the Top 3 industries, sector-level risk should be monitored alongside individual borrower risk.

Use the branch risk matrix for prioritization
Give highest priority to branches that combine high outstanding exposure and high overdue ratios.

Monitor upcoming maturity proactively
Use maturity buckets and contract watchlists to identify potential repayment pressure before contracts become overdue.

Track risk together with portfolio growth
Growth should not be evaluated independently from overdue exposure trends.

Technical Highlights

This project demonstrates several Power BI and DAX techniques:

Multiple date-role analysis across disbursement date, repayment due date, actual repayment date, and maturity date

Historical AS-OF calculations

Active and inactive relationship management

USERELATIONSHIP for alternative date paths

CROSSFILTER and REMOVEFILTERS for filter-context control

TREATAS for virtual filtering between repayment schedule and actual repayment logic

Iterator functions such as SUMX and MAXX

Pareto analysis using RANKX, TOPN, and ALLSELECTED

KPI variance and forecast analysis

Branch-level risk segmentation

Customer and industry concentration analysis

Maturity-bucket analysis

Contract-level watchlist logic

Project Limitations

The project was developed for academic and portfolio purposes.

Risk-status thresholds are analytical assumptions and do not represent official regulatory loan-classification rules.

Some repayment records do not contain repayment-period identifiers (KY), therefore installment-level repayment matching is treated as an analytical proxy where applicable.

The current Power BI tenant does not allow public Publish to Web embed-code creation, so the repository provides dashboard screenshots and the PBIX file instead.

Raw banking data is not included in the repository.

Repository Structure

Credit-Contract-Portfolio-Risk-Analytics/
│
├── README.md
├── PowerBI/
│   └── Credit_Contract_Portfolio_Risk_Analytics.pbix
│
├── Screenshots/
│   ├── page01_portfolio_overview.png
│   ├── page02_disbursement_kpi.png
│   ├── page03_repayment_collection.png
│   └── page04_portfolio_risk.png
│
├── Docs/
│   └── Credit_Contract_Portfolio_Risk_Analytics_VI.docx
│
└── Data/
    └── README.md

How to Open the Power BI Dashboard

Download:

PowerBI/Credit_Contract_Portfolio_Risk_Analytics.pbix

Open the file using Microsoft Power BI Desktop.

Use the available slicers to explore the report by:

reporting period;

region;

branch;

industry.

Documentation

Detailed project documentation is available in:

Docs/Credit_Contract_Portfolio_Risk_Analytics_VI.docx

Portfolio Value

This project demonstrates the ability to move from raw banking data to management-oriented analytics across four levels:

Business Understanding
        ↓
Data Modeling
        ↓
DAX & Analytical Logic
        ↓
Dashboard & Business Insights

The final solution connects descriptive analytics, KPI monitoring, repayment analysis, concentration risk, and actionable credit monitoring in a single Power BI project.
