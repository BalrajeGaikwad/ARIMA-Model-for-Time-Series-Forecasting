ARIMA Model for time series forecasting. ARIMA model is used to forecast a time series using the series past values. In this notebokk, we build an optimal ARIMA model and extend it to Seasonal ARIMA (SARIMA) and SARIMAX models. We will also see how to build autoarima models in python.

1. Introduction to Time Series Forecasting ¶

- A Time Series is defined as a series of data points recorded at different time intervals. The time order can be daily, monthly, or even yearly.
- Time Series forecasting is the process of using a statistical model to predict future values of a time series based on past results.
- We have discussed various aspects of Time Series Forecasting in the previous notebook - Complete Guide to Time Series Analysis in Python.
- Forecasting is the step where we want to predict the future values the series is going to take. Forecasting a time series is often of tremendous commercial value.
  
Forecasting a time series can be broadly divided into two types.
- If we use only the previous values of the time series to predict its future values, it is called Univariate Time Series Forecasting.
- If we use predictors other than the series (like exogenous variables) to forecast it is called Multi Variate Time Series Forecasting.
- This notebook focuses on a particular type of forecasting method called ARIMA modeling.
