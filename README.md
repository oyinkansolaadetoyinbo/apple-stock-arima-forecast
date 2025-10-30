# 📈 Time Series Modelling of Apple Inc. Share Prices

This repository presents a **Time Series Analysis and Forecasting** of **Apple Inc.’s daily closing stock prices** using the **ARIMA model** in R.  
It demonstrates how historical financial data can be used to model trends, test stationarity, perform model diagnostics, and forecast future prices.

---

## 🎯 Objectives

- Explore and visualize Apple Inc.’s stock price trends.  
- Test for **stationarity** using the Augmented Dickey-Fuller (ADF) test.  
- Build and evaluate **ARIMA** models for time-series forecasting.  
- Perform **residual diagnostics** to validate model adequacy.  
- Generate **30-day forecasts** with confidence intervals.

---

## 📊 Dataset Overview

The dataset spans several decades of Apple’s daily trading activity with columns:

- `Date`  
- `Open`, `High`, `Low`, `Close`  
- `Adjusted Close`  
- `Volume`  

For this analysis, only the **Close price** was used because it reflects market sentiment at the end of each trading day.

---

## 🧮 Methods

### 1️⃣ Data Visualization
```r
ggplot(close_prices, aes(x = Date, y = Close)) +
  geom_line(color = "blue") +
  labs(title = "Apple Inc. Close Price Over Time",
       x = "Date", y = "Close Price") +
  theme_minimal()
Time Series Decomposition
close_ts <- ts(close_prices$Close, start = c(1980, 12), frequency = 252)
decomposed_ts <- decompose(close_ts)
plot(decomposed_ts)
The decomposition reveals a strong upward trend, little to no seasonality, and random residuals (noise).
Stationarity Testing
adf_test <- adf.test(close_ts, alternative = "stationary")
p-value > 0.05 → non-stationary

Differencing applied → achieves stationarity
ARIMA Modelling
model <- auto.arima(close_ts)
summary(model)
The auto.arima() function automatically selects the best-fit ARIMA(p, d, q) model using the AIC criterion.

5️⃣ Model Diagnostics
checkresiduals(model)
Residual diagnostics confirmed independence and normality, validating the model fit.

6️⃣ Forecasting
forecasted_values <- forecast(model, h = 30)
plot(forecasted_values)


Forecast results aligned with the historical upward trend, indicating continued growth potential.

✅ Key Findings

Apple’s stock shows a strong long-term upward trend driven by innovation and market confidence.

The ARIMA model achieved good predictive accuracy and reliability.

Diagnostics confirmed model adequacy and validity of assumptions.

💡 Recommendations

Investors: Use ARIMA forecasts for short-term trading insights.

Future Work: Integrate macroeconomic variables (market indices, inflation).

Maintenance: Update the model regularly with new data.

📚 References

Cheng, D. et al. (2022). Financial time series forecasting with multi-modality graph neural network. Pattern Recognition, 121, 108218. https://doi.org/10.1016/j.patcog.2021.108218

Kaur, J., Parmar, K.S., & Singh, S. (2023). Autoregressive models in environmental forecasting time series: a theoretical and application review. Environmental Science and Pollution Research, 30(8), 19617–19641. https://doi.org/10.1007/s11356-023-25148-9

🧠 Author

Oyin
Data Analyst & Researcher
📧 [https://www.linkedin.com/posts/oyinkansola-adetoyinbo]
🧾 License

MIT License © 2025 Oyin
You are free to use, modify, and distribute with proper attribution.
