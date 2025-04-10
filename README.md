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

2. Introduction to ARIMA Models

- ARIMA stands for Autoregressive Integrated Moving Average Model. It belongs to a class of models that explains a given time series based on its own past values -i.e.- its own lags and the lagged forecast errors. The equation can be used to forecast future values. Any ‘non-seasonal’ time series that exhibits patterns and is not a random white noise can be modeled with ARIMA models.
- So, ARIMA, short for AutoRegressive Integrated Moving Average, is a forecasting algorithm based on the idea that the information in the past values of the time series can alone be used to predict the future values.
- ARIMA Models are specified by three order parameters: (p, d, q),
 where,

p is the order of the AR term

q is the order of the MA term

d is the number of differencing required to make the time series stationary

- AR(p) Autoregression – a regression model that utilizes the dependent relationship between a current observation and observations over a previous period. An auto regressive (AR(p)) component refers to the use of past values in the regression equation for the time series.
- I(d) Integration – uses differencing of observations (subtracting an observation from observation at the previous time step) in order to make the time series stationary. Differencing involves the subtraction of the current values of a series with its previous values d number of times.
- MA(q) Moving Average – a model that uses the dependency between an observation and a residual error from a moving average model applied to lagged observations. A moving average component depicts the error of the model as a combination of previous error terms. The order q represents the number of terms to be included in the model.

- Types of ARIMA Model¶
 - ARIMA : Non-seasonal Autoregressive Integrated Moving Averages
 - SARIMA : Seasonal ARIMA
 - SARIMAX : Seasonal ARIMA with exogenous variables
If a time series, has seasonal patterns, then we need to add seasonal terms and it becomes SARIMA, short for Seasonal ARIMA.

3. The meaning of p, d and q in ARIMA model

  3.1 The meaning of p¶
- p is the order of the Auto Regressive (AR) term. It refers to the number of lags of Y to be used as predictors.
  3.2 The meaning of d¶
- The term Auto Regressive’ in ARIMA means it is a linear regression model that uses its own lags as predictors. Linear regression models, as we know, work best when the predictors are not correlated and are independent of each other. So we need to make the time series stationary.
- The most common approach to make the series stationary is to difference it. That is, subtract the previous value from the current value. Sometimes, depending on the complexity of the series, more than one differencing may be needed.
- The value of d, therefore, is the minimum number of differencing needed to make the series stationary. If the time series is already stationary, then d = 0.

  3.3 The meaning of q
- q is the order of the Moving Average (MA) term. It refers to the number of lagged forecast errors that should go into the ARIMA Model.
- 

4.1 AR model¶
- An Auto Regressive (AR) model is one where Yt depends only on its own lags.
- That is, Yt is a function of the lags of Yt. It is depicted by the following equation

4.2 MA model¶
- Likewise a Moving Average (MA) model is one where Yt depends only on the lagged forecast errors. It is depicted by the following equation -

4.3 ARIMA model¶
- An ARIMA model is one where the time series was differenced at least once to make it stationary and we combine the AR and the MA terms. So the equation of an ARIMA model becomes :

5. How to find the order of differencing (d) in ARIMA model

- As stated earlier, the purpose of differencing is to make the time series stationary. But we should be careful to not over-difference the series. An over differenced series may still be stationary, which in turn will affect the model parameters.
- So we should determine the right order of differencing. The right order of differencing is the minimum differencing required to get a near-stationary series which roams around a defined mean and the ACF plot reaches to zero fairly quick.
- If the autocorrelations are positive for many number of lags (10 or more), then the series needs further differencing. On the other hand, if the lag 1 autocorrelation itself is too negative, then the series is probably over-differenced.
- If we can’t really decide between two orders of differencing, then we go with the order that gives the least standard deviation in the differenced series.
- Now, we will explain these concepts with the help of an example as follows:-
- First, I will check if the series is stationary using the Augmented Dickey Fuller test (ADF Test), from the statsmodels package. The reason being is that we need differencing only if the series is non-stationary. Else, no differencing is needed, that is, d=0.
- The null hypothesis (Ho) of the ADF test is that the time series is non-stationary. So, if the p-value of the test is less than the significance level (0.05) then we reject the null hypothesis and infer that the time series is indeed stationary.
- So, in our case, if P Value > 0.05 we go ahead with finding the order of differencing.
