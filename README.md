# 🛒 E-Commerce Sales Performance Analysis
### End-to-End Transactional Data Analysis for a UK-Based Online Retail Business

<br>

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.x-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=for-the-badge)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-4C8CBF?style=for-the-badge)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [Business Objectives](#-business-objectives)
- [Dataset Information](#-dataset-information)
- [Tools & Technologies](#-tools--technologies)
- [Project Workflow](#-project-workflow)
- [Key Analyses Performed](#-key-analyses-performed)
- [Key Insights](#-key-insights)
- [Business Recommendations](#-business-recommendations)
- [Visualizations](#-visualizations)
- [Folder Structure](#-folder-structure)
- [How to Run the Project](#-how-to-run-the-project)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 📌 Project Overview

This project presents a **comprehensive, end-to-end sales performance analysis** of a UK-based online retail business using 12 months of transactional invoice data spanning **December 2010 to December 2011**.

### The Business Problem

The retailer — a wholesale and B2C gift and homewares business selling across 37 countries — lacked structured visibility into the key drivers of its revenue performance. Leadership needed answers to critical questions: *Which customers drive the most value? Which products are underperforming? Is the business retaining customers after acquisition? Where is geographic revenue risk concentrated?*

### Purpose of the Analysis

This analysis was designed to transform raw transactional records into **executive-grade business intelligence**, covering:

- Revenue trends and seasonality patterns
- Customer segmentation and lifetime value distribution
- Retention dynamics through cohort analysis
- Product portfolio performance
- Geographic revenue concentration and international opportunity

### Value of the Project

Rather than descriptive reporting alone, this project delivers **prescriptive analytics** — translating every finding into a concrete, prioritised business recommendation. The result is a decision-support asset suitable for executive review, commercial strategy, and marketing operations.

---

## 🎯 Business Objectives

| # | Business Question | Analysis Approach |
|---|-------------------|-------------------|
| 1 | What are the monthly and seasonal revenue trends? | Monthly revenue trend analysis with peak annotation |
| 2 | Which markets generate the most revenue — and what is the geographic concentration risk? | Country-level revenue aggregation and UK share calculation |
| 3 | How does order value fluctuate across the year? | Average Order Value (AOV) monthly trend analysis |
| 4 | What is the purchase frequency profile of the customer base? | Customer frequency distribution histogram |
| 5 | Which customers generate disproportionate lifetime value? | CLV distribution analysis on log scale |
| 6 | How well does the business retain customers after first purchase? | Monthly cohort retention heatmap |
| 7 | Which customers are Champions, Loyal, At Risk, or Lost? | RFM (Recency, Frequency, Monetary) scoring & segmentation |
| 8 | Which products are the strongest revenue drivers? | Product-level revenue ranking |
| 9 | Which products are systematically underperforming? | Revenue-per-transaction product efficiency analysis |
| 10 | What is the optimal day of week to drive revenue? | Day-of-week revenue aggregation analysis |

---

## 📦 Dataset Information

| Attribute | Detail |
|-----------|--------|
| **Source** | [Kaggle — E-Commerce Data (UCI Online Retail)](https://www.kaggle.com/carrie1/ecommerce-data) |
| **Business Type** | UK-based gift & homewares online retailer |
| **Raw Rows** | 541,909 invoice-level transaction records |
| **Columns** | 8 features |
| **Period** | December 2010 – December 2011 |
| **Currency** | British Pounds (£) |
| **Geography** | 37 countries |
| **Format** | CSV (ISO-8859-1 encoding) |

### Data Dictionary

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `InvoiceNo` | String | Unique invoice identifier. Prefix `C` denotes a cancellation/return | `536365`, `C536379` |
| `StockCode` | String | Unique product/SKU identifier | `85123A`, `71053` |
| `Description` | String | Human-readable product name | `WHITE HANGING HEART T-LIGHT HOLDER` |
| `Quantity` | Integer | Units per transaction line. Negative = return | `6`, `-1` |
| `InvoiceDate` | DateTime | Invoice timestamp | `12/1/2010 8:26` |
| `UnitPrice` | Float | Price per unit in British Pounds (£) | `2.55`, `3.39` |
| `CustomerID` | Float/Int | Unique customer identifier. **135,080 rows null** (guest/untracked orders) | `17850` |
| `Country` | String | Customer's country | `United Kingdom`, `Germany` |

### Dataset Characteristics

- **Missing Data:** 135,080 rows (~25%) lack a `CustomerID`, representing guest or untracked orders — these were excluded from customer-centric analyses
- **Cancellations:** Invoices prefixed with `C` represent order returns and were removed from revenue calculations
- **Negative Quantities:** Rows with zero or negative quantity/price were filtered to isolate genuine forward transactions
- **Clean Dataset Shape:** ~397,000 rows after cleaning, with 4,338 unique customers and 3,877 unique products across 36 countries

---

## 🛠 Tools & Technologies

| Category | Tools |
|----------|-------|
| **Language** | Python 3.10+ |
| **Data Manipulation** | Pandas, NumPy |
| **Visualisation** | Matplotlib, Seaborn |
| **Development Environment** | Jupyter Notebook |
| **Data Source** | Kaggle (UCI ML Repository) |
| **Output** | PNG chart exports, clean CSV export |

---

## 🔄 Project Workflow

### Phase 1 — Data Collection
Raw transactional CSV data was sourced from the Kaggle UCI Online Retail dataset. The file was loaded with `ISO-8859-1` encoding and parsed with datetime inference applied to the `InvoiceDate` column. Initial shape, date range, column types, and missing value counts were inspected to map data quality issues before processing.

### Phase 2 — Data Cleaning
A multi-stage cleaning pipeline was applied:
- **Cancellation removal:** All invoices prefixed with `C` (returns) were excluded
- **Null CustomerID drop:** Rows without a `CustomerID` were removed to enable customer-level analysis
- **Invalid record filter:** Rows with `Quantity ≤ 0` or `UnitPrice ≤ 0` were excluded
- **Type correction:** `CustomerID` cast from float to integer for clean aggregation

The cleaning pipeline reduced the dataset from 541,909 raw rows to a structurally valid, analysis-ready core dataset.

### Phase 3 — Feature Engineering
New analytical variables were derived from existing fields:
- `Revenue` — computed as `Quantity × UnitPrice` for every transaction line
- `Year`, `Month`, `MonthName`, `DayOfWeek`, `YearMonth` — temporal decomposition from `InvoiceDate`
- `CohortMonth` — each customer's first-ever purchase month, used as their cohort identifier
- `TransactionMonth` — month of each individual transaction
- `CohortIndex` — integer offset (months since first purchase) enabling retention curve construction
- `Quarter` — Q1–Q4 classification for seasonal analysis
- `Segment` — RFM-derived customer classification (Champions, Loyal, Potential Loyalists, At Risk, Lost)

### Phase 4 — Exploratory Data Analysis
Structured EDA was conducted across four analytical domains: sales performance, customer behaviour, product portfolio, and retention. Each domain was addressed with dedicated aggregations and visualisations before business interpretation.

### Phase 5 — Visualisation
10 publication-quality charts were produced using a custom visual theme (deep navy, burnt orange, sky blue, slate) applied consistently across all figures. Charts were exported as 150 DPI PNG files to a dedicated `/charts` directory.

### Phase 6 — Insight Generation
Every analysis section concludes with an interpretive narrative block that contextualises the statistical finding in business terms — avoiding bare numbers and focusing on implication and risk.

### Phase 7 — Recommendations
Seven prioritised, actionable business recommendations were synthesised from the analytical findings, covering CRM strategy, inventory planning, international growth, and product merchandising.

---

## 🔍 Key Analyses Performed

**Sales Performance Analysis**
- Monthly revenue trend from Dec 2010 to Dec 2011 with peak-value annotation, revealing a strong Q4 seasonal surge to over £1.2M in November 2011
- Top 10 countries by total revenue with UK share calculation (83% concentration identified)
- Revenue by day of week, revealing Thursday as the peak trading day

**Customer Behaviour Analysis**
- Average Order Value (AOV) by month, with overall mean of £369 and median of £230 — exposing a right-skewed distribution driven by large wholesale orders
- Purchase frequency distribution (capped at 20 orders for visualisation clarity), showing ~35% one-time buyers and a median of 2 orders per customer
- Customer Lifetime Value (CLV) distribution plotted on a log₁₀ scale, revealing strong Pareto concentration — top 10% of customers generated £2,800+ in lifetime revenue

**Cohort Retention Analysis**
- Monthly cohort retention heatmap covering 13 months of cohort observation, quantifying month-1, month-3, and month-6 retention rates — average month-1 retention found to be 20–25%

**RFM Customer Segmentation**
- Composite RFM scoring (R + F + M quintiles) used to classify all customers into five named segments: Champions, Loyal Customers, Potential Loyalists, At Risk, and Lost
- Dual visualisation: customer count per segment and total revenue contribution per segment

**Product Portfolio Analysis**
- Top 10 products by total revenue, concentrated in decorative homewares and seasonal gifting
- 10 most underperforming products by average revenue per transaction (minimum 20 transactions threshold applied to remove low-frequency noise)

---

## 💡 Key Insights

**1. UK Market Dominance — Geographic Concentration Risk**
> 
![Top Countries by Revenue](charts/02_top_countries.png)

> 83% of total revenue originates from a single market (United Kingdom). This level of geographic concentration constitutes material strategic risk if domestic demand softens.

**2. Q4 Seasonality — Narrow Revenue Window**
> 
![Q4 Seasonality](charts/01_monthly_revenue.png)

> Revenue spikes sharply in October–November, driven by Christmas gifting preparation. The business is disproportionately dependent on a 6–8 week trading window, creating both an opportunity and an operational vulnerability.

**3. Champions Drive ~70% of Revenue — Pareto Concentration**
>
![Champions Drive](charts/10_rfm_segments.png)
> 
> Just 934 customers (the Champions RFM segment) generated approximately £6.25M. Losing even a fraction of this segment would have an outsized negative impact on total revenue.

**4. Low First-Month Retention — Retention is the #1 Growth Lever**
>
> ![Low First-Month Retention](charts/09_cohort_retention.png)
> 
> Average month-1 retention sits at just 20–25%, declining steeply thereafter. The first 30 days post-acquisition represent the most critical and currently under-utilised engagement window.

**5. Thursday is the Peak Trading Day**
>
> ![Thursday is Peak Trading Day](charts/03_day_of_week.png)
> 
> Thursday consistently records the highest single-day revenue across all months in the analysis period, presenting a clear opportunity for campaign timing alignment.

**6. ~35% of Customers Are One-Time Buyers**
>
> ![35% One-Time Buyers](charts/05_purchase_frequency.png)
> 
> A significant proportion of the customer base makes a single purchase and does not return. Given the cost of customer acquisition, first-to-second purchase conversion is a high-ROI retention opportunity.

**7. AOV Rises Materially in Q4 — Upsell Window Exists**
>
> ![AOV Rises in Q4](charts/04_aov_monthly.png)
>
> Average Order Value increases significantly during Q4 due to larger gift-driven basket sizes. This seasonal AOV uplift is not yet being systematically exploited through upsell or bundle strategies.

---

## 📋 Business Recommendations

### 1. 🏆 Protect & Grow Champions
- Launch a **VIP loyalty tier** with exclusive early access to new products and free delivery
- Assign dedicated account support or relationship management to the top 100 customers by CLV
- Implement personalised product recommendations informed by purchase history and recency data

### 2. 🔁 Re-engage At-Risk Customers (≈800 customers, £430K at stake)
- Deploy a **multi-touchpoint win-back email sequence**: discount coupon → product spotlight → urgency nudge
- Use live RFM scores to trigger re-engagement automations before customers migrate to the "Lost" segment

### 3. 🛒 Convert One-Time Buyers to Repeat Buyers
- Trigger a **post-purchase nurture sequence** at 14, 30, and 60 days after first order
- Offer a first-repeat-order incentive (e.g., 10% off second purchase) with defined expiry to create urgency

### 4. 📅 Capitalise on Q4 Seasonality
- Pre-stock top 10 SKUs by September with at least 2× normal inventory buffers
- Launch paid media campaigns in **late September** — ahead of the competitor spend spike
- Create gift bundle SKUs at clear price points: £25, £50, £75

### 5. 🌍 Accelerate Geographic Diversification
- Invest in country-specific landing pages and localised marketing for the top 5 international markets (Netherlands, Germany, France, EIRE, Australia)
- Evaluate European fulfilment partnerships to reduce shipping time and friction for EU customers

### 6. 📆 Optimise Campaign Timing by Day of Week
- Schedule promotional emails and paid advertisements on **Tuesdays and Thursdays** to align with peak buyer intent
- Explore Saturday/Sunday flash sale mechanics to lift weekend revenue, which currently underperforms

### 7. 📦 Address Underperforming Products
- Review pricing strategy for products with very low average revenue per transaction
- Bundle low-revenue-per-transaction items with top-selling products to increase basket size
- Consider discontinuing SKUs generating less than £2 average revenue per transaction

---

## 📊 Visualizations

| # | Chart | Key Finding |
|---|-------|-------------|
| 01 | **Monthly Revenue Trend** | Steady growth Jan–Oct 2011; sharp Q4 peak at £1.2M+ in November |
| 02 | **Top 10 Countries by Revenue** | UK accounts for 83% of total revenue; Netherlands, Germany, France are the top international markets |
| 03 | **Revenue by Day of Week** | Thursday is the peak revenue day; Sunday is the weakest |
| 04 | **Average Order Value by Month** | Overall mean AOV = £369; median = £230; Q4 AOV materially elevated |
| 05 | **Purchase Frequency Distribution** | ~35% of customers are one-time buyers; median = 2 orders; max = 209 orders |
| 06 | **CLV Distribution (Log₁₀ Scale)** | Highly right-skewed; median CLV = £370; top 10% = £2,800+ |
| 07 | **Top 10 Products by Revenue** | Decorative homewares and seasonal gifting dominate the top revenue SKUs |
| 08 | **Underperforming Products** | Several SKUs with 20+ transactions generating <£2 avg revenue per transaction |
| 09 | **Cohort Retention Heatmap** | Month-1 retention ≈ 20–25%; Dec 2010 cohort (holiday buyers) shows strongest long-term retention |
| 10 | **RFM Segmentation** | Champions (934 customers) generate ~£6.25M; At-Risk segment (≈800 customers) represents £430K of recoverable revenue |

> 📁 All charts are saved as 150 DPI PNG files in the `/charts` directory.

---

## 📁 Folder Structure

```
E-Commerce-Sales-Performance-Analysis/
│
├── 📂 charts/
│   ├── 01_monthly_revenue.png
│   ├── 02_top_countries.png
│   ├── 03_day_of_week.png
│   ├── 04_aov_monthly.png
│   ├── 05_purchase_frequency.png
│   ├── 06_clv_distribution.png
│   ├── 07_top_products.png
│   ├── 08_underperforming.png
│   ├── 09_cohort_retention.png
│   └── 10_rfm_segments.png
│
├── 📂 data/
│   ├── data.csv                    # Raw dataset (source from Kaggle)
│   └── data_clean.csv              # Cleaned & feature-engineered export
│
├── 📂 dashboard/
│   ├── ecommerce_dashboard.pbix     # Power BI dashboard
│   └── ecommerce_dashboard.PNG      # dashboard screenshot
│
├──  📂 docs/
│     ├── ecommerce_analysis_presentation.pptx   # Powerpoint slide
│     └── ecommerce_report.docx                  # project documentation
│
├──  📓 notebook/
│     ├── ecommerce_analysis.ipynb     # Main analysis notebook
│
└── 📄 README.md                    # Project documentation
```

---

## ▶️ How to Run the Project

### Prerequisites

Ensure you have **Python 3.8+** and **Jupyter Notebook** or **JupyterLab** installed.

### Step 1 — Clone the Repository

```bash
git clone https://github.com/onyemarihappy/E-Commerce-Sales-Performance-Analysis.git
cd E-Commerce-Sales-Performance-Analysis
```

### Step 2 — Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Or, if using a `requirements.txt`:

```bash
pip install -r requirements.txt
```

### Step 3 — Download the Dataset

Download the dataset from [Kaggle](https://www.kaggle.com/carrie1/ecommerce-data) and place `data.csv` in the `/data` folder.

### Step 4 — Update the File Path

In the notebook cell under **Section 2 — Data Loading**, update the file path to match your local environment:

```python
df_raw = pd.read_csv("data/data.csv", encoding='ISO-8859-1', parse_dates=['InvoiceDate'])
```

### Step 5 — Run the Notebook

```bash
jupyter notebook ecommerce_analysis.ipynb
```

Run all cells sequentially (`Kernel → Restart & Run All`) to reproduce the full analysis and regenerate all charts in the `/charts` directory.

---

## 🚀 Future Improvements

- **Predictive CLV Modelling** — Apply probabilistic models (BG/NBD + Gamma-Gamma) to forecast future customer lifetime value and churn probability
- **Market Basket Analysis** — Use association rule mining (Apriori / FP-Growth) to identify product affinity pairs and inform cross-sell bundle strategies
- **Time-Series Forecasting** — Build a Prophet or ARIMA model to forecast monthly revenue and flag anomalies in real time
- **Interactive Dashboard** — Port the analysis to a Plotly Dash or Power BI dashboard for live stakeholder self-service
- **Churn Prediction** — Train a binary classifier (XGBoost, Logistic Regression) on RFM features to predict which customers are likely to churn in the next 30/60/90 days
- **A/B Test Simulation** — Model the revenue impact of the proposed win-back and upsell recommendations using hypothesis testing frameworks
- **Automated RFM Refresh** — Build a pipeline to recalculate RFM scores on a rolling basis as new transactions arrive

---

## 👤 Author

<table>
  <tr>
    <td>
      <strong>Happiness Onyemari</strong><br>
      Passionate about turning raw transactional data into commercial intelligence. Focused on Python-based analytics, customer segmentation, and building business cases from data.<br><br>
      📧 <a href="mailto:onyemarih93@gmail.com">onyemarih93@gmail.com</a><br>
      🐙 <a href="https://github.com/onyemarihappy">GitHub</a><br>
    </td>
  </tr>
</table>

---

## 📜 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- Dataset sourced from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/online+retail) via Kaggle, originally published by Dr. Daqing Chen, School of Engineering, London South Bank University.

---

<p align="center">
  ⭐ If you found this project useful, please consider giving it a star on GitHub!
</p>
