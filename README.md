 # Insurance_dashboard

# Insurance Premium & Payout KPI Dashboard (Power BI) 
End-to-end finance analytics project built in Power BI to analyze insurance premiums, payouts and policy performance for a fictitious company, True Secure Credit Insurance (2015–2025).

## 1. Business Problem

TruSecure Credit Insurance wants a single dashboard to:
- Track total premiums (paid, payable and total) across policies and states.
- Monitor key KPIs like maturity amount, ROI, CAGR and underwriting expenses.
- Analyze policy-wise, state-wise and agent-wise performance.
- Identify underperforming policy types and improve claim/loan processes.
- Provide management with an always up-to-date, automated view of the business.

## 2. Data & Modeling

- Source: Client-style specification and CSV files (customer, policy, policy type, agents, regional/zonal managers, fact policy table).
- Volume: ~10,000 policy records plus multiple dimension tables (customers, policies, agents, managers, etc.).
- Model: Star schema with:
  - Fact table: `Fact_InsurancePolicy`
  - Dimension tables: `Dim_Customer`, `Dim_Policy`, `Dim_PolicyType`, `Dim_Agent`, `Dim_RegionManager`, `Dim_ZonalManager`
- Relationships: Many-to-one, single or bi-directional where required for cross-filtering (e.g. Agent → Customer via Fact).

## 3. Key Metrics & DAX

Some of the main measures implemented:

- **Total Premium Amount**: Total premium over full tenure (premium × tenure).
- **Total Premium Paid**: Amount paid so far based on start date and current year.
- **Total Premium Payable**: Remaining premium (total – paid).
- **Maturity Amount**: Based on policy type, tenure, status and premium, using a return-rate matrix.
- **Annualized ROI**: Average return rate per year from maturity value, total invested and number of years.
- **CAGR** (Compound Annual Growth Rate): Growth of investment over time assuming compounding. 

Logic:
- Premium payment duration, premium frequency normalization (monthly, quarterly, half-yearly, yearly via SWITCH logic).
- Filters to consider only *active* policies for certain KPIs.

## 4. Power BI Features Used

- Power Query for:
  - Importing multiple CSV files (dimension and fact tables).
  - Cleaning header rows, removing junk rows, selecting relevant columns.
  - Converting text columns to numeric types (underwriting expense, premium amount, sum assured).

- Data Modeling:
  - Star schema design with clear fact/dimension separation.
  - Relationship management (one-to-many, bi-directional where needed).
  - Use of dimension tables to reduce model size instead of merging everything into the fact table.

- DAX & Analytics:
  - Time-intelligence (YTD/MTD/YoY).
  - ROI and CAGR calculations.
  - KPI measures for premiums, maturity, underwriting expenses and growth.

- Security & UX:
  - Row-Level Security (RLS) based on agent/region/state.
  - Drill-through pages for policy, state and agent-level details.
  - Slicers for policy type, state, tenure and time period.

## 5. Dashboard Views

The Power BI report consists of multiple analytical pages, each designed to answer a specific business question for management, operations, and sales leadership.


1️⃣ Summary (Executive KPI View)

Purpose:
Provides a high-level snapshot of overall insurance business performance.

Key Highlights:

Total number of policies

Total premium amount

Total annual premium

Total premium paid vs payable

Total underwriting expenses

Quick filters for policy type, policy name, agent, year, state, and occupation

Tabular KPI breakdown for quick comparisons


Business Value:
Enables top management to quickly assess revenue, liabilities, and cost efficiency in one glance.

2️⃣ Insurance Overview

Purpose:
Analyzes premium composition, growth trends, and underwriting performance.

Key Insights:

Annual premium distribution by policy type

Fixed vs variable annual premium growth

Total premium amount, paid, and payable trends

Underwriting expense contribution over time

Comparative charts showing premium growth patterns


Business Value:
Helps identify high-performing policy types and monitor expense control effectiveness.


3️⃣ Investment Value vs Maturity Value

Purpose:
Evaluates long-term investment performance of insurance policies.

Key Insights:

Total premium paid vs maturity amount by year

Annualized ROI trends over time

Comparison of investment value growth against maturity returns

Correlation between premium investment and expected payout


Business Value:
Supports financial planning and helps assess policy attractiveness and customer value creation.


4️⃣ Annual Premium vs Protection Value

Purpose:
Compares customer investment with insurance coverage value.

Key Insights:

Annual premium vs sum assured (coverage amount)

Growth in protection value over policy tenure

Risk-to-reward comparison across policy types

Identification of policies with high protection at optimized premium cost


Business Value:
Assists product teams in improving policy pricing and protection offerings.


5️⃣ Premium Analysis (5–20 Years)

Purpose:
Analyzes premium behavior over long-term policy durations.

Key Insights:

Premium accumulation trends across 5–20 year tenures

Long-term growth patterns in premium paid and payable

Impact of tenure length on maturity and ROI

Identification of profitable long-duration policies


Business Value:
Helps in designing long-term insurance products and retention strategies.


6️⃣ Sales Hierarchy Analysis

Purpose:
Provides a hierarchical performance view from zonal managers down to individual sales agents.

Key Insights:

Zonal manager → Regional manager → Sales agent drill-down

Total premium, paid, payable, and underwriting expenses by hierarchy

Agent-wise contribution to revenue

Performance comparison across regions and teams


Business Value:
Supports sales performance tracking, incentive planning, and managerial accountability.
