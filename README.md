                              📊📈 Retail Sales & Demand Forecasting 📊📈

A time-series forecasting project using Facebook Prophet to predict future store-level sales, incorporating holiday effects across 1,115 stores.

📌 Project Overview

This project analyzes retail store sales data using Python to understand sales performance, seasonality, and store-level trends.

The project uses merged store, sales, and transaction-level data — **1,017,209 records across 1,115 stores**.

The analysis focuses on data cleaning, correlation analysis, and building a validated, backtested forecasting model per store.

🎯 Project Objectives

- Clean and merge store, sales, and holiday-calendar data
- Identify which factors actually correlate with sales
- Analyze seasonal and store-type sales patterns
- Build a per-store sales forecasting model using Facebook Prophet
- Backtest the forecast against real held-out data with a quantified error metric

🛠️ Technologies Used

🐍 Python
- Data analysis

📊 Pandas & NumPy
- Data cleaning, merging, and preprocessing

📈 Matplotlib & Seaborn
- Sales trend and pattern visualization

📓 Jupyter Notebook
- Exploratory analysis and forecasting

🔮 Facebook Prophet
- Time-series forecasting with holiday effects

📁 Dataset

- 📊 1,017,209 sales records across **1,115 stores** (classic Rossmann Store Sales dataset)
- 🔑 Fields: Store, Date, Sales, Customers, Open, Promo, StateHoliday, SchoolHoliday, StoreType, Assortment, CompetitionDistance

🔍 Data Cleaning & Preparation

- Cleaned missing values in store-level metadata (competition distance, promo timing fields)
- Merged sales data with store metadata and holiday calendars (school and state holidays)

🔍 Correlation Analysis

Analyzed which factors actually correlate with sales across all 1,017,209 records:

| Feature | Correlation with Sales |
|---|---|
| **Customers** | **+0.824** (strongest driver) |
| Promo | +0.368 |
| SchoolHoliday | +0.039 |
| DayOfWeek | −0.179 |
| Promo2 (extended promo) | −0.128 |
| CompetitionDistance | −0.036 |

The clear takeaway: foot traffic (Customers) drives sales far more than any other single factor, and running a Promo has a real, meaningful positive effect. Extended/ongoing promotions (Promo2), interestingly, correlate *negatively* — a specific, counterintuitive finding worth digging into further.

📈 Forecasting & Backtesting

- Built per-store sales forecasts using **Facebook Prophet**, incorporating school and state holiday effects as model regressors
- **Backtested against real held-out data** — trained on all but the last 60 days per store, then measured forecast accuracy against those actual held-out days:

  **Store 6 backtest result:**
  - MAE: **752.87**
  - RMSE: **916.48**
  - **MAPE: 16.55%**

- Note: 50 of the 60 held-out days had matching forecast dates for Store 6 (10 days had no match, likely store-closure gaps in the historical data) — handled safely via a merge rather than crashing on the mismatch

💡 Key Business Insights

- **Customer foot traffic is by far the strongest driver of sales** (correlation 0.824) — far stronger than any other factor measured
- Running a promotion has a real, positive effect on sales (+0.368 correlation), while extended/ongoing promotions show the opposite pattern — worth investigating why
- The Prophet forecast for Store 6 achieved a **16.55% MAPE** on 60 days of genuinely unseen data, meaning predictions were off by about 1 in 6 on average — solid for a single-store baseline with room to improve using store-specific tuning
- Store-level sales history has real-world gaps (closures), which the backtesting pipeline now handles safely instead of crashing

⭐ Project Highlights

📊 Records Analyzed: 1,017,209

🏬 Stores Covered: 1,115

🔗 Strongest Sales Driver: Customer count (correlation 0.824)

📈 Forecasting Model: Facebook Prophet (with holiday regressors)

✅ Backtested Accuracy (Store 6, 60-day holdout): MAPE 16.55%, RMSE 916.48
