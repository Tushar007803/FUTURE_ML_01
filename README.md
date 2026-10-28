# FUTURE_ML_01 – Sales & Demand Forecasting for Businesses

> **Future Interns – Machine Learning Internship | Task 1**

## 📌 Overview

This project builds a machine learning model that forecasts future monthly sales for a retail business using historical order data from the **Superstore** dataset. It turns raw transaction records into a monthly time series, engineers time-based and lag features, trains a Random Forest regressor, evaluates it on unseen months, and produces a business-ready 3-month sales forecast.

---

## 🎯 Problem Statement

Businesses need to know how much they are likely to sell in the coming months to plan inventory, staffing, and budgets. Without a reliable forecast, they risk overstocking, stock-outs, and missed revenue.

**Task:** Build a model to forecast future sales using historical business data, evaluate it, and present the forecast with clear visuals and insights.

---

## 🚀 Features

- Data Cleaning (date/number parsing, duplicate removal, sorting by date)
- Aggregating transactions into a monthly sales time series
- Time-based Feature Engineering (Year, Month, Lag-1, Lag-2, Lag-3)
- Chronological Train/Test Split (no data leakage)
- Forecasting with a Random Forest Regressor
- Model Evaluation (MAE, RMSE) and Error Analysis
- 3-month Future Sales Forecast with Business Report
- Visual outputs: trend, actual vs predicted, and forecast charts

---

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

---

## 📊 Dataset

**Sample – Superstore** (`Sample - Superstore.csv`): **9,994 orders** and **21 columns**, covering **January 2014 to December 2017**.

| Column | Description |
|---|---|
| Row ID, Order ID | Row and order identifiers |
| Order Date, Ship Date | Order and shipping dates |
| Ship Mode | Shipping method |
| Customer ID, Customer Name, Segment | Customer details and segment |
| Country, City, State, Postal Code, Region | Location details |
| Product ID, Category, Sub-Category, Product Name | Product details |
| **Sales** | Sales amount (forecast target) |
| Quantity, Discount, Profit | Units sold, discount applied, profit |

There are no missing values in the dataset. Only `Order Date` and `Sales` are used for forecasting.

---

## 🧹 Methodology

1. **Data cleaning** – converted `Order Date` to datetime and `Sales` to numeric, dropped invalid rows and duplicates, and sorted by date.
2. **Monthly aggregation** – total sales resampled by month, giving **48 monthly data points**.
3. **Feature engineering** – extracted `Year` and `Month`, and created `Lag_1`, `Lag_2`, `Lag_3` (sales of the previous 1, 2, and 3 months). After removing the rows lost to lagging, **45 rows** remain.
4. **Train/test split** – first 80% of months for training (**36**) and the last 20% for testing (**9**, April–December 2017). The split is chronological, so the model never sees the future.
5. **Model** – `RandomForestRegressor(n_estimators=200, max_depth=5, random_state=42)`.
6. **Forecasting** – the next 3 months (Jan–Mar 2018) are predicted recursively: each prediction is fed back in as a lag feature for the next month.

---

## 📈 Model Performance

| Metric | Value |
|---|---:|
| MAE (Mean Absolute Error) | 14,458.66 |
| RMSE (Root Mean Squared Error) | 19,320.03 |

**Error analysis (test period, Apr–Dec 2017)**

- The model tracks the general level and direction of sales well, for example May and December are predicted closely.
- It **under-predicts the sharp seasonal peaks**, most notably November 2017 (actual ≈ 118K vs predicted ≈ 77K). This is the main driver of the RMSE.
- With only 36 training months, the model has seen just three holiday seasons, which limits how well it learns the strong Q4 spike.

---

## 🔮 Forecast (Next 3 Months)

| Month | Predicted Sales |
|---|---:|
| January 2018 | 26,308.36 |
| February 2018 | 33,608.21 |
| March 2018 | 42,733.86 |

- **Total forecast sales:** 102,650.43
- **Average monthly sales:** 34,216.81
- **Highest predicted month:** March 2018 (42,733.86)



## 💡 Business Insights

- Sales show a clear **seasonal pattern**, with the strongest months at the end of the year (Sept–Dec) and weaker months at the start (Jan–Feb). Inventory and staffing should be ramped up ahead of Q4.
- The forecast for early 2018 suggests a **slow start to the year followed by a recovery in March**, so promotions in January and February could help lift demand.
- Because the model under-predicts peak months, planners should treat its output as a **baseline** and add a safety buffer for high-demand periods.

---

## ▶️ How to Run

1. Clone the repository
2. Install dependencies

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
```

3. Place `Sample - Superstore.csv` in the same folder as the notebook
4. Open the notebook

```bash
jupyter notebook FUTURE_ML_01.ipynb
```

---

## 📌 Future Improvements

- Add more history-aware features (rolling averages, seasonal indicators, holiday flags)
- Compare against classical time-series models (ARIMA / SARIMA, Prophet)
- Use time-series cross-validation (`TimeSeriesSplit`) and hyperparameter tuning
- Forecast by Category or Region for more granular planning
- Build an interactive dashboard in Power BI or Tableau

---

## 👨‍💻 Author

Tushar Thorat

Machine Learning Intern at **Future Interns**


