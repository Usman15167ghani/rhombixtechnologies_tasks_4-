# Sales Forecasting for a Retail Store (Walmart)

A time-series project that analyzes historical weekly sales of Walmart stores, finds useful business insights, and forecasts future sales using four different models.

This project was completed as an internship task at **Rhombix Technologies**.

---

## Project Goal

Use past sales data to predict future sales, so a retail business can plan its inventory and staffing better. The project covers data cleaning, visual analysis, model building, model comparison, and a 12-week future forecast.

## Dataset

- **File:** `Walmart.csv`
- **Size:** 6,435 rows, 8 columns
- **Stores:** 45 Walmart stores
- **Period:** February 2010 to October 2012 (143 weeks)

| Column | Description |
|---|---|
| Store | Store number (1 to 45) |
| Date | Week ending date |
| Weekly_Sales | Sales for that store in that week |
| Holiday_Flag | 1 if the week has a special holiday, otherwise 0 |
| Temperature | Average temperature in the region |
| Fuel_Price | Fuel cost in the region |
| CPI | Consumer Price Index |
| Unemployment | Unemployment rate |

## Steps in the Project

1. Import libraries and load the data
2. Clean the data (fix date format, check missing values and duplicates)
3. Explore the data with charts
4. Find key insights
5. Prepare the data for forecasting (last 20 weeks kept for testing)
6. Build four models: ARIMA, SARIMA, Holt-Winters and Prophet
7. Compare the models using MAE, RMSE and MAPE
8. Forecast the next 12 weeks with the best model

## Key Insights

- **Strong seasonality:** December sales are about 39% higher than January sales.
- **Busiest week:** The week before Christmas is the best week every year, with about $77M to $81M in total sales across all stores.
- **Holiday flag can mislead:** Thanksgiving weeks are about 40% above normal, but the flagged Christmas week (ending Dec 31) is weak. The real Christmas peak is the unflagged week before it.
- **Big gap between stores:** The best store (Store 20) sells about 8 times more per week than the weakest store (Store 33).
- **Economic factors matter little:** Temperature, fuel price, CPI and unemployment have very weak correlation with sales.

![Total weekly sales](images/sales_trend.png)

![Average weekly sales by store](images/store_sales.png)

## Model Results

The models were trained on the first 123 weeks and tested on the last 20 weeks.

| Model | MAE | RMSE | MAPE |
|---|---|---|---|
| **Holt-Winters** | 1,001,996 | 1,222,770 | **2.14%** |
| SARIMA | 1,006,703 | 1,268,744 | 2.16% |
| Prophet | 1,058,311 | 1,447,258 | 2.24% |
| ARIMA | 1,473,058 | 1,970,559 | 3.22% |

Holt-Winters was the most accurate, with SARIMA and Prophet very close behind. ARIMA was the weakest because it has no seasonal part and predicts an almost flat line, so it misses the yearly sales pattern.

![Actual vs predicted sales](images/model_predictions.png)

## 12-Week Forecast

The best model (Holt-Winters) was used to forecast total weekly sales from November 2012 to January 2013:

- Early November: about $47M to $48M per week
- Thanksgiving week (ending Nov 23): about $67.6M
- Week before Christmas (ending Dec 21): about $82.1M, the yearly peak
- January: about $43M to $45M per week

![12-week forecast](images/forecast_12_weeks.png)

## Business Recommendations

1. Build inventory and staffing ahead of Thanksgiving and especially the week before Christmas.
2. Plan for a slow January by reducing stock orders and adjusting staff hours.
3. Do not rely only on the Holiday_Flag column for planning.
4. Review the weakest stores (33, 44 and 5) and learn from the strongest ones (20, 4 and 14).

## Tools Used

- Python
- Pandas and NumPy
- Matplotlib and Seaborn
- Statsmodels (ARIMA, SARIMA, Holt-Winters)
- Prophet
- Scikit-learn (error metrics)
- Jupyter Notebook

## How to Run

1. Clone the repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

2. Install the required libraries

```bash
pip install pandas numpy matplotlib seaborn statsmodels prophet scikit-learn jupyter
```

3. Make sure `Walmart.csv` is in the same folder as the notebook, then open it

```bash
jupyter notebook Walmart_Sales_Forecasting.ipynb
```

## Project Structure

```
.
├── Walmart_Sales_Forecasting.ipynb
├── Walmart.csv
├── images/
│   ├── sales_trend.png
│   ├── store_sales.png
│   ├── model_predictions.png
│   └── forecast_12_weeks.png
└── README.md
```

## Future Improvements

- Forecast each store separately instead of the total
- Add holiday dates as extra inputs to Prophet
- Try an LSTM neural network and compare it with these models

## Author

**Your Name**
[LinkedIn](https://www.linkedin.com/in/your-profile) | [GitHub](https://github.com/your-username)
