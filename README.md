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


### 1️⃣ Data Visualization
```r
ggplot(close_prices, aes(x = Date, y = Close)) +
  geom_line(color = "blue") +
  labs(
    title = "Apple Inc. Close Price Over Time",
    x = "Date",
    y = "Close Price"
  ) +
  theme_minimal()


The plot above shows Apple’s daily closing stock prices over time.
It reveals a strong upward trend—especially from the 2000s onward—driven by innovation and global market expansion.

2️⃣ Time Series Decomposition
close_ts <- ts(close_prices$Close, start = c(1980, 12), frequency = 252)
decomposed_ts <- decompose(close_ts)
plot(decomposed_ts)


The decomposition separates the data into:

Trend: steady long-term growth pattern.

Seasonality: minimal, as stock prices are influenced more by market events than fixed seasonal cycles.

Residuals: random noise capturing short-term fluctuations.

3️⃣ Stationarity Testing
adf_test <- adf.test(close_ts, alternative = "stationary")


p-value > 0.05 → non-stationary, meaning the series has a trend.

Applying first-order differencing makes the data stationary — a prerequisite for ARIMA modelling.

4️⃣ ARIMA Modelling
model <- auto.arima(close_ts)
summary(model)


The auto.arima() function automatically selects the best-fitting ARIMA(p, d, q) model using the AIC criterion.
This approach ensures an optimal balance between model accuracy and complexity.

5️⃣ Model Diagnostics
checkresiduals(model)


Residual diagnostics confirmed:

Independence (no autocorrelation)

Constant variance

Approximate normality

---

## 📊 Results and Discussion

The ARIMA model successfully captured Apple Inc.’s stock price dynamics, showing a strong alignment between historical trends and forecasted values.  
The 30-day forecast continued the upward trajectory seen in the historical data, reflecting investor confidence and Apple’s sustained innovation.

Key observations:
- **Consistent Growth:** The model reinforced Apple’s long-term upward momentum, with only minor fluctuations linked to external market events.  
- **Model Accuracy:** Metrics such as RMSE and MAPE demonstrated strong predictive reliability.  
- **Residual Validation:** Diagnostics confirmed that residuals were normally distributed and uncorrelated, ensuring the model’s stability.  
- **Forecast Reliability:** Confidence intervals revealed that short-term forecasts are dependable for investor and analyst insights, though uncertainty increases over longer horizons.

This outcome validates the suitability of ARIMA for short-term stock forecasting and demonstrates its potential in financial time series modeling.

---

## 🧾 Conclusion and Recommendations

The ARIMA-based time series analysis of Apple Inc.’s stock prices effectively demonstrated how historical patterns can forecast short-term market behavior.  
The model met key assumptions of stationarity and independence, produced accurate predictions, and provided valuable decision-making insights for investors.

### 🔹 Recommendations
- **For Investors:** Use ARIMA forecasts for short-term trading signals while continuously monitoring real-world events that could disrupt trends.  
- **For Analysts:** Incorporate additional explanatory variables (e.g., NASDAQ index, inflation rate, global market indicators) to enhance predictive accuracy.  
- **For Ongoing Work:** Update the model regularly with new data to maintain relevance and reliability as market conditions evolve.

---

## 📚 References

- Cheng, D. et al. (2022). *Financial time series forecasting with multi-modality graph neural network.* **Pattern Recognition, 121**, 108218. [https://doi.org/10.1016/j.patcog.2021.108218](https://doi.org/10.1016/j.patcog.2021.108218)

- Kaur, J., Parmar, K.S., & Singh, S. (2023). *Autoregressive models in environmental forecasting time series: a theoretical and application review.* **Environmental Science and Pollution Research, 30(8)**, 19617–19641. [https://doi.org/10.1007/s11356-023-25148-9](https://doi.org/10.1007/s11356-023-25148-9)

--

## 👤 Author

**Oyin**  
_Data Analyst & Researcher_  
📊 [GitHub Profile](https://github.com/oyinkansolaadetoyinbo)




