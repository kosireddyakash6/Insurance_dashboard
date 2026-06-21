

# **PROJECT: TRUSECURE INSURANCE BUSINESS PERFORMANCE DASHBOARD**

## **1. Business Problem Understanding**

TruSecure is a prominent insurance provider managing complex risk profiles, premium cycles, and multi-layered sales distributions. To transition away from legacy tracking processes, this enterprise business intelligence project analyzes exactly **7,299 active insurance policies** representing **39,096.58M in Gross Premium Volume** to optimize underwriting margins, identify policyholder decay, and track agent productivity.

The analytics framework targets **4 critical operational challenges**:

* **High Customer Attrition Risk:** An advanced RFM behavioral model reveals that **57.2% of the entire customer base falls into the "At Risk" segment**, exposing **$213,249,790 in baseline premium revenue** to potential churn.
* **Premium Realization Leakage:** Out of 39.09B in total premium value, there is a substantial lag in cash realization, with **28,410.24M currently sitting in outstanding "Premium Payable" accounts** versus only **10,686.35M in "Premium Paid"**.
* **Sales Hierarchy Underperformance:** A major performance delta exists across sales channels, highlighting a critical operational dependence on a small group of high-performing Zonal and Regional managers.
* **Data Processing Latency:** Manual report compilation previously consumed significant analyst bandwidth weekly, delaying critical risk assessments and policy distribution insights.

The overarching objective was to build a secure, automated data engineering and visualization ecosystem in Microsoft Fabric and Power BI to surface deep portfolio insights, automate data workflows, and support targeted customer retention campaigns.

---

## **2. Project Architecture & Data Modeling**

I architected an enterprise-grade **Star Schema** to power high-speed analytical filtering, dynamic parameter slicing, and quick cross-report execution:

* **Fact Table:** `Fact_Policies` containing **7,299 distinct rows** tracking transactional policy metrics. Core numeric indicators include `Premium_Amount`, `Total_Annual_Premium`, `Total_Premium_Paid`, `Total_Premium_Payable`, `Underwriting_Expense`, `Sum_Assured_INR`, and `Maturity_Amount`.
* **Dimension Tables:** Contextual boundaries were decoupled into independent lookup entities to maintain lightweight data storage:
* `Dim_Customers`: Stores policyholder demographics, customer names, occupations, and unique IDs.
* `Dim_Sales_Hierarchy`: Maps corporate sales tiers linking *Zonal Managers*, *Regional Managers*, and *Sales Agents*.
* `Dim_Policy_Metadata`: Stores policy classifications split by *Policy Type* (Endowment, Universal, Whole) and unique *Policy Name* structures.
* `Dim_Geography`: Groups territorial parameters by *State* and regional sales boundaries.
* `Dim_Date`: A dedicated corporate calendar table powering advanced time-intelligence calculations.



Relational associations utilize strict **Many-to-One (`*:1`) Cardinality** mapping from the central policy fact table out to the dimensional contexts. Cross-filter directions are kept as **Single** to maintain strict query paths and protect against performance degradation during massive calculations.

---

## **3. Data Sources & Automated ETL Pipeline**

The backend data pipeline was built entirely within the cloud-native **Microsoft Fabric Ecosystem** to automate data processing and eliminate manual maintenance loops:

* **Data Integration Pipeline:** Developed an automated **Fabric Refresh_Pipeline** that orchestrates data movement smoothly.
* **Dataflow Transformation Layer:** Ingested raw operational source files into an **Insurance Dataflow** engine. Transformations included removing dirty text headers, casting exact currency formatting types across financial metrics, and handling structural missing values.
* **Semantic Refresh Automation:** Configured a successful downstream link connecting the completed dataflow directly to an automated **Semantic Model Refresh trigger**.
* **Orchestration Scheduling:** Scheduled a **Fixed Daily Refresh Loop** running on a 1-month recurrence interval, synchronized to local corporate time zones `(UTC+05:30) Chennai, Kolkata, Mumbai`. This cloud architecture successfully saves analysts **3–4 hours of manual effort weekly**.

---

## **4. Power BI Dashboard Design**

I designed an executive-ready application featuring a responsive multi-tab layout tailored for risk management and financial tracking:

### **Page 1: Policy Executive Summary**

* **Analytics Focus:** A dense operational ledger providing micro-level policy audits. Displays critical top-level metrics including **7,299 Policies**, **39.09bn Premium Amount**, and **38.66M Underwriting Expenses** alongside a detailed policyholder tabular grid.
<img width="1538" height="499" alt="Insurance_Summary-Page 1 (1)" src="https://github.com/user-attachments/assets/2ba6e270-e31f-4e45-8013-fe5937959dcd" />

---

### **Page 2: Premium Performance & Portfolio Overview**

* **Analytics Focus:** Breaks down corporate numbers by product line, showing that **Endowment Policies (34.89%)**, **Whole Life (33.17%)**, and **Universal Policies (31.94%)** share revenue evenly. Includes horizontal tree-maps ranking sales agents and geographical charts mapping state-level volume contributions.
<img width="1354" height="723" alt="Insurance_Overview-Page 2 (1)" src="https://github.com/user-attachments/assets/fa3c1c95-bee0-4223-8137-59654a84576d" />

---

### **Page 3: Longitudinal Investment & Maturity Forecasting**

* **Analytics Focus:** Plots financial metrics chronologically over extended time horizons. Tracks actual premium collection trends against long-term maturity projections across a multi-year landscape.
<img width="1281" height="725" alt="Investment_value vs Maturity_value -Page 3 (1)" src="https://github.com/user-attachments/assets/12ed5f53-f655-4249-a1e5-cda25d50f802" />

---

### **Page 4: Coverage Value vs. Pricing Calibration**

* **Analytics Focus:** A dynamic time-intelligence view tracking annual premium amounts against long-term protection values over a historical trendline. It shows a steep upward trajectory in average annualized ROI metrics, topping out at a **671.25M premium baseline by 2024**.
<img width="1405" height="726" alt="Annual Premium vs Protection value -Page 4 (1)" src="https://github.com/user-attachments/assets/f74141e6-ce8f-4001-b134-4b974ed75860" />

---

### **Page 5: Premium Lifecycle Horizon Analysis**

* **Analytics Focus:** Tracks cash flow risk over time. Isolates upcoming revenue schedules by clustering paid premiums against outstanding balances, categorized by specific payment buckets.
<img width="1090" height="533" alt="Premium_Analysis(5 - 20 years) - Page 5 (1)" src="https://github.com/user-attachments/assets/cff4434f-6eff-4468-be3f-115fe69060e2" />

---

### **Page 6: Multi-Tiered Sales Hierarchy Leaderboard**

* **Analytics Focus:** A matrix view mapping corporate leadership tiers. Allows direct drill-downs from *Zonal Managers* (e.g., Rohit Kapoor, Lakshmi Iyer) down through *Regional Managers* (e.g., Ananya Sharma, Naveen Verma) directly down to individual *Sales Agents* (e.g., Baiju Singh, Divij Malhotra). This view surfaces exactly who is driving the **2.16B Total Annual Premium volume**.
<img width="1134" height="602" alt="Sales_Hierarchy - Page 6" src="https://github.com/user-attachments/assets/d8893483-88d8-4325-9259-f5d8d6f74fc5" />

---

### **Page 7: Advanced RFM Customer Segmentation**

* **Analytics Focus:** An executive analytical radar screen built using behavioral grouping logic. Isolates high-value customers from churn risks, explicitly highlighting that **4.193K customers** sit within the vulnerable **"At Risk" segment**.
<img width="1382" height="813" alt="Insurance_RFM_Analysis" src="https://github.com/user-attachments/assets/f21169d6-4137-45c7-8c62-a5b5d5a7bd25" />

---

## **5. KPIs & Advanced DAX Measures**

I authored robust, optimized DAX formulas to run the complex underlying calculations behind TruSecure's visuals:

* **Aggregated Portfolio Underwriting Expense:**

```dax
Underwriting expense = SUM(Fact_Policies[Underwriting_Expense])

```

* **Net Realized Cash Inflow:**

```dax
Total Premium Paid = SUM(Fact_Policies[Total_Premium_Paid])

```

* **Outstanding Premium Receivables Balance:**

```dax
Total Premium Payable = SUM(Fact_Policies[Total_Premium_Payable])

```

* **Premium Realization Efficiency Metric Percentage:**

```dax
% Premium Paid = 
DIVIDE(
    [Total Premium Paid], 
    [Total Premium Amount], 
    0
) * 100

```

* **Dynamic Sales Force Hierarchy Ranking:**

```dax
Agent Performance Rank = 
RANKX(
    ALL(Dim_Sales_Hierarchy[Sales_Agent]), 
    [Total Annual Premium], 
    , 
    DESC, 
    DENSE
)

```

---

## **6. Business Insights & Recommendations**

1. **Mitigate the 57.2% At-Risk Churn Window:** Behavioral RFM grouping shows that **$213.2M in premium volume is vulnerable** within the "At Risk" category. **Action:** Launch automated email and text reminder triggers 45 days prior to policy renewal timelines, specifically targeting this customer segment.
2. **Close the Premium Payable Realization Gap:** Out of a 39.09B total premium baseline, an oversized **28.41B remains outstanding in payable accounts**. **Action:** Incentivize digital autopay setups by offering small premium discounts (0.5%–1%) to convert slow manual invoicing cycles into predictable automatic cash inflows.
3. **Address Sales Hierarchy Production Variances:** Cross-filtering the hierarchical leaderboard highlights that key regional hubs under specific managers generate a large share of annual volumes, while others lag. **Action:** Standardize the sales techniques used by top producers like *Baiju Singh* and *Divij Malhotra* into a mandatory training playbook to lift baseline performance across underperforming regional teams.
4. **Rebalance the Product Mix Allocation:** Revenue contributions are evenly split across Endowment, Whole, and Universal policies. **Action:** Since market demand is balanced, focus marketing spend on the specific policy tiers that demonstrate the lowest historical underwriting expenses to maximize net profitability.
