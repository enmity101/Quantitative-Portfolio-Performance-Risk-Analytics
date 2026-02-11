# Quantitative Portfolio Performance & Risk Analytics

---

## Executive Summary

This repository presents a rigorous, institutional-grade quantitative framework for evaluating investment portfolio performance, risk exposure, and benchmark-relative returns. The analytical pipeline integrates structured data extraction via SQL, preprocessing and exploratory analysis in Microsoft Excel and Python, advanced quantitative modeling in Python (Jupyter Notebook), and executive-level visualization through Power BI dashboards.

The system is designed to support investment decision-making processes by delivering precise, reproducible metrics across the dimensions of return attribution, volatility characterization, risk-adjusted performance, and capital allocation efficiency. Output artifacts are intended for consumption by portfolio managers, risk officers, and senior investment analysts.

---

## Project Objectives

The primary analytical objectives of this repository are as follows:

- Measure absolute and benchmark-relative portfolio returns across defined evaluation periods
- Quantify portfolio volatility and characterize the return distribution profile
- Compute standard and extended risk-adjusted performance metrics, including the Sharpe Ratio, Sortino Ratio, and Calmar Ratio
- Identify and analyze maximum drawdown episodes and recovery periods
- Evaluate portfolio outperformance (alpha) relative to designated benchmark indices
- Segment holdings by risk classification (Low, Medium, High) and assess contribution to total portfolio risk
- Analyze transaction-level data to identify volume trends, cost effects, and rebalancing efficiency
- Aggregate portfolio valuations over time and assess the compounding trajectory of capital

---

## Methodology

### 1. Data Extraction (SQL)

Raw portfolio data — including transaction records, position-level holdings, pricing history, and benchmark index levels — is extracted from a relational database using structured SQL queries. Queries are parameterized to support configurable date ranges and asset universe filters. Extracted datasets are exported in flat-file formats (CSV) for downstream processing.

All SQL scripts are located in the `sql/` directory and are documented with inline commentary describing table schemas, join logic, and filter conditions.

### 2. Data Preprocessing (Excel / Python)

Initial data quality assessment and exploratory analysis are conducted in Microsoft Excel. This stage encompasses missing value identification, outlier flagging, date alignment, and preliminary summary statistics. Preprocessed datasets are validated before ingestion into the Python modeling environment.

Within Python, the `pandas` library is used for systematic data cleaning, type enforcement, index normalization, and feature engineering. This includes the derivation of daily return series, rolling window calculations, and categorical risk tier assignments.

### 3. Quantitative Modeling (Python — Jupyter Notebook)

The core analytical computations are implemented in Python within a structured Jupyter Notebook environment. The modeling pipeline executes the following:

- Computation of period returns (daily, monthly, quarterly, annualized)
- Volatility estimation using both realized standard deviation and exponentially weighted moving averages (EWMA)
- Rolling Sharpe Ratio and drawdown series generation
- Benchmark comparison via tracking error and information ratio computation
- Distribution analysis including skewness, kurtosis, and Value-at-Risk (VaR) estimation
- Correlation matrix construction across portfolio constituents
- Risk segmentation and contribution analysis by asset class and risk tier

### 4. Visualization (Power BI)

Processed analytical outputs are imported into Power BI for dashboard-level visualization. Dashboards are structured to serve multiple stakeholder audiences, from operational portfolio review to senior management reporting. Visual components include equity curves, drawdown charts, rolling risk-return scatter plots, benchmark comparison overlays, and transaction volume analytics.

### 5. Risk and Return Computation Logic

Return series are computed on a total-return basis, accounting for dividends and distributions where applicable. Annualization of volatility follows the square-root-of-time convention using 252 trading days per year. Risk-adjusted metrics are computed against the risk-free rate using the prevailing short-term rate for the evaluation period. Drawdown is computed on a peak-to-trough basis from the cumulative return series.

---

## Scope of Analysis

**Absolute and Relative Portfolio Returns**
- Cumulative and annualized total returns over defined evaluation periods
- Periodic return decomposition (daily, monthly, quarterly, annual)
- Benchmark-relative excess return series

**Volatility and Drawdown Analysis**
- Realized annualized volatility (rolling and point-in-time)
- EWMA volatility estimation with configurable decay factor
- Maximum drawdown, duration, and recovery period analysis
- Underwater curve visualization

**Risk-Adjusted Performance Metrics**
- Sharpe Ratio (excess return per unit of total volatility)
- Sortino Ratio (excess return per unit of downside deviation)
- Calmar Ratio (annualized return divided by maximum drawdown)
- Information Ratio (active return per unit of tracking error)

**Benchmark Outperformance**
- Alpha estimation relative to designated benchmark indices
- Tracking error and active return distribution
- Percentage of periods with positive active return

**Trend Analysis**
- Rolling performance attribution across market regimes
- Momentum and mean-reversion signal characterization
- Return persistence analysis

**Risk Segmentation**
- Asset classification into Low, Medium, and High risk tiers based on individual volatility
- Risk contribution analysis by segment and constituent
- Concentration metrics and diversification ratio

**Transaction Volume Analytics**
- Trade frequency and notional volume aggregation
- Turnover rate computation by period and asset class
- Transaction cost impact estimation

**Portfolio Value Aggregation**
- Mark-to-market portfolio valuation over the full evaluation period
- Compounded growth curve and capital efficiency metrics
- Asset-level and portfolio-level attribution of value changes

---

## Financial Metrics: Definitions and Methodology

**Volatility**
Volatility refers to the annualized standard deviation of portfolio returns. It quantifies the dispersion of returns around their mean and serves as the primary measure of total portfolio risk. This analysis employs both unconditional (historical) volatility and conditional volatility via EWMA to capture regime-dependent risk dynamics.

**Sharpe Ratio**
The Sharpe Ratio measures the risk-adjusted return of the portfolio, defined as the excess return over the risk-free rate divided by the annualized standard deviation of returns. A higher Sharpe Ratio indicates superior return per unit of total risk assumed. The metric assumes returns are approximately normally distributed and penalizes both upside and downside volatility equally.

**Drawdown**
Drawdown measures the decline from a portfolio's peak cumulative value to a subsequent trough, expressed as a percentage loss. Maximum drawdown identifies the largest such peak-to-trough decline over the full evaluation period. Drawdown analysis is critical for assessing tail risk and the resilience of the portfolio under adverse market conditions.

**Risk-Return Tradeoff**
The risk-return tradeoff characterizes the relationship between expected portfolio return and the associated level of risk. Efficient portfolios maximize expected return for a given level of risk (or equivalently, minimize risk for a given return target). This analysis assesses portfolio positioning along the efficient frontier and evaluates whether compensation for risk borne is adequate relative to benchmarks and peer portfolios.

**Benchmark Alpha and Outperformance**
Alpha represents the portfolio's return in excess of that predicted by its benchmark exposure. Positive alpha is interpreted as evidence of active management value-add beyond passive market exposure. The information ratio contextualizes this outperformance by scaling alpha by tracking error, providing a measure of the consistency and efficiency of active return generation.

---

## Repository Structure

```
quantitative-portfolio-analytics/
│
├── data/
│   ├── raw/                        # Source data extracted from SQL queries
│   ├── processed/                  # Cleaned and transformed datasets (CSV)
│   └── benchmarks/                 # Benchmark index price series
│
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_return_computation.ipynb
│   ├── 03_volatility_modeling.ipynb
│   ├── 04_risk_adjusted_metrics.ipynb
│   ├── 05_drawdown_analysis.ipynb
│   ├── 06_benchmark_comparison.ipynb
│   ├── 07_risk_segmentation.ipynb
│   └── 08_transaction_analytics.ipynb
│
├── sql/
│   ├── extract_transactions.sql
│   ├── extract_holdings.sql
│   ├── extract_pricing.sql
│   └── extract_benchmarks.sql
│
├── dashboards/
│   ├── portfolio_performance.pbix   # Power BI dashboard file
│   └── exports/                     # Static PDF/PNG exports of dashboards
│
├── excel/
│   ├── data_validation.xlsx
│   └── exploratory_analysis.xlsx
│
├── reports/
│   ├── performance_summary.pdf
│   └── risk_report.pdf
│
├── requirements.txt
└── README.md
```

---

## How to Run the Project

### Prerequisites

- Python 3.9 or higher
- pip package manager
- Jupyter Notebook or JupyterLab
- Access to the source database (for SQL extraction)
- Microsoft Power BI Desktop (for dashboard rendering)

### Environment Setup

**Step 1: Clone the Repository**

```bash
git clone https://github.com/<your-org>/quantitative-portfolio-analytics.git
cd quantitative-portfolio-analytics
```

**Step 2: Create a Python Virtual Environment**

```bash
python -m venv venv
```

Activate the virtual environment:

- On macOS/Linux:
  ```bash
  source venv/bin/activate
  ```
- On Windows:
  ```bash
  venv\Scripts\activate
  ```

**Step 3: Install Dependencies**

```bash
pip install -r requirements.txt
```

**Step 4: Configure Database Connection**

Update the database connection parameters in `sql/config.py` (or the relevant configuration file) with the appropriate host, credentials, and schema references. The project uses `SQLAlchemy` for database connectivity, supporting PostgreSQL, MySQL, and SQLite backends.

**Step 5: Execute SQL Extraction Scripts**

Run the SQL extraction scripts to populate the `data/raw/` directory. These may be executed directly against the target database using a preferred SQL client, or programmatically via the notebook `01_data_preprocessing.ipynb`.

**Step 6: Launch Jupyter Notebook**

```bash
jupyter notebook
```

Navigate to the `notebooks/` directory and execute notebooks in sequential order (01 through 08) to reproduce the full analytical pipeline.

**Step 7: Connect Power BI to Processed Data**

Open `dashboards/portfolio_performance.pbix` in Power BI Desktop. Update the data source path to reference the processed CSV files in `data/processed/`. Refresh the data model to populate the dashboards with current analytical outputs.

---

## Technical Stack

| Component             | Tool / Library                        | Purpose                                               |
|-----------------------|---------------------------------------|-------------------------------------------------------|
| Data Extraction       | SQL (PostgreSQL / MySQL / SQLite)     | Structured query and transformation of source data    |
| Data Preprocessing    | Microsoft Excel                       | Initial validation, exploratory review                |
| Quantitative Analysis | Python 3.9+ / Jupyter Notebook        | Return, risk, and attribution modeling                |
| Data Manipulation     | pandas, numpy                         | Tabular operations, vectorized computation            |
| Statistical Modeling  | scipy, statsmodels                    | Distribution fitting, regression, hypothesis testing  |
| Visualization         | matplotlib, seaborn                   | Static charts and analytical plots                    |
| BI Dashboard          | Microsoft Power BI Desktop            | Interactive performance dashboards                    |
| DB Connectivity       | sqlalchemy                            | Database abstraction and query execution              |
| Excel I/O             | openpyxl                              | Programmatic Excel file read/write                    |
| Notebook Runtime      | jupyter                               | Interactive computational environment                 |

---

## Use Cases

**Investment Performance Review**
Systematic evaluation of portfolio returns across multiple time horizons, enabling portfolio managers to assess period performance, identify outperformance drivers, and track progress against stated investment objectives.

**Portfolio Optimization Review**
Assessment of current asset allocation against the efficient frontier, with identification of holdings that introduce excess risk without commensurate return contribution. Outputs support rebalancing decisions and allocation strategy refinement.

**Institutional Risk Monitoring**
Ongoing quantification of portfolio-level and constituent-level risk exposures, including volatility, drawdown, VaR, and risk tier classifications. Designed to support compliance, risk management, and investment committee reporting requirements.

**Strategic Asset Allocation Analysis**
Evaluation of long-term capital allocation decisions through the lens of risk-adjusted return, benchmark tracking, and diversification efficiency. Supports top-down asset class selection and tactical weighting adjustments.

---

## Notes on Reproducibility

All analytical computations are implemented in a deterministic, fully reproducible manner. Random seeds are fixed where applicable. Notebook outputs are version-controlled to enable audit-trail validation. Data inputs are stored with timestamps to ensure traceability from raw extraction to final reporting outputs.

---

## License

This repository is proprietary. Unauthorized distribution, reproduction, or use of this codebase outside the intended organizational context is prohibited without explicit written consent.

---

*Maintained by the Quantitative Research and Analytics Group.*
