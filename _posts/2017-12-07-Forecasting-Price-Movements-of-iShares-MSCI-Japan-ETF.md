This post presents a simple time series analysis of [iShares MSCI Japan ETF (EWJ)](https://www.ishares.com/us/products/239665/ishares-msci-japan-etf) using autoregressive integrated moving average (ARIMA) models to forecast future price movements.

The iShares MSCI Japan ETF seeks to track the investment results of MSCI Japan Index, which consists of stocks traded primarily on the Tokyo Stock Exchange. A summary prospectus can be found [here](https://www.ishares.com/us/library/stream-document?stream=reg&product=WEBXJPY&shareClass=NA&documentId=925856~926146~926374~1180074~1242907&iframeUrlOverride=%2Fus%2Fliterature%2Fsummary-prospectus%2Fsp-ishares-msci-japan-etf-8-31.pdf).

> *The full R code for the following analysis can be found [here](http://roywangtw.github.io/files/2017-12-07-Forecasting-Price-Movements-of-iShares-MSCI-Japan-ETF.nb.html).*

## Data retrieval and exploration

Due to the limits on data retrieval from Yahoo! Finance, our data dates back to only January 03, 2017.

```
library(quantmod) 
library(dplyr) 
ts <- getSymbols("EWJ", src = "yahoo", auto.assign = FALSE) %>% Cl() # Retrieve and extract the ETF's closing price data from Yahoo! Finance
sum(is.na(ts)) # Check for missing data
head(ts) # View the first few rows
tail(ts) # View the last few rows
dim(ts) # Check the numbers of rows and columns
frequency(ts) # Check the number of observations per unit time
```

![center](http://roywangtw.github.io/images/2017-12-07-load-examine-raw-data.png)

In sum, our data contains 2753 observations and 1 column, with 1 day for each unit time, spanning from January 03, 2007 to December 06, 2017, which adds up to 10.91 years.

The ETF's past performance is shown below.

```
library(xts)
plot.xts(ts, main = "iShares MSCI Japan ETF - Closing Prices", col = "darkblue", auto.legend = TRUE, legend.loc = "bottomright") # Plot the ETF's historical closing prices
```

![center](http://roywangtw.github.io/images/2017-12-07-ETF-timeplot.png)

The ETF suffered a huge downturn that saw its net asset value more than halved during the 2008 financial crisis before climbing back again to new highs as of early December, 2017.

## Time series analysis

It is clear from the timeplot above the closing prices' time series is anything but stationary, as it wanders up and down over for sustained periods. A formal Augmented Dickey-Fuller (ADF) test below also does not reject the null hypothesis of non-stationarity.

```
library(tseries) # Load the tseries package for Augmented Dickey-Fuller Test
adf.test(ts, alternative = "stationary") # Run the ADF test to verify stationarity
```

![center](http://roywangtw.github.io/images/2017-12-07-ADF-test.png)

Therefore, we need to take the first difference of the time series, which involves subtracting the previous entry's value from the value of the current period.

```
ts.diff <- diff(ts)[-1, ] # Take the first difference on the time series and remove the first row which contains NA
head(ts.diff) # Check the first few rows
ts.plot(ts.diff) # Plot the new differenced series
adf.test(ts.diff, alternative = "stationary") # Run the ADF test to verify stationarity
```

![center](http://roywangtw.github.io/images/2017-12-07-load-examine-differenced-series.png)

![center](http://roywangtw.github.io/images/2017-12-07-differenced-series-plot.png)

The plot of our new differenced series shows an oscillating pattern around zero with no visible clear trend. More importantly, the ADF test result rejects the null hypotheses of non-stationarity, suggesting the series most likely conforms to stationarity and thus differencing of order 1 is sufficient.

Regarding the order parameters for ARIMA modeling, the autocorrelation function (ACF) plot below indicates significant autocorrelations at lag 1 and 16, while the partial autocorrelation function (PACF) plot points out significant autocorrelations at lag 1, 2, 5, and beyond.

```
par(mar = c(4, 4, 4, 4)) # Adjust for the right graphic margins
acf(ts.diff, main = "ACF for Differenced Series") # Check for MA lags
pacf(ts.diff, main = "PACF for Differenced Series") # Check for AR lags
```

![center](http://roywangtw.github.io/images/2017-12-07-ACF-differenced-series.png)

![center](http://roywangtw.github.io/images/2017-12-07-PACF-differenced-series.png)

Then we apply the original time series of the ETF's closing prices to the **`auto.arima`** function.

```
library(forecast) # Load the forecast package for fitting the series data to the ARIMA model
ts.arima <- auto.arima(ts) %>% # Fit and print out the ARIMA model
  print()
```

![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-first-model.png)

The result recommends ARIMA(3,1,4) model. However, before we rush to make some forecasts, we need to examine the ACF and PACF plots for model residuals to see if this ARIMA(3,1,4) model is trustworthy enough.

```
checkresiduals(ts.arima) # Check the model residuals for normality and autocorrelations
qqnorm(ts.arima$residuals, asp = 1) # Check the model residuals' QQ plot to inspect normality
qqline(ts.arima$residuals, asp = 1)
```

![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-first-model-Ljung-test.png)


![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-first-model-residuals.png)


![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-first-model-qqplot.png)

The Ljung-Box test returns a significant p-value for model residuals, and the ACF plot indicates significant autocorrelations at lag 8, 16, and beyond. Both the histogram and the QQ plot for model residuals point towards non-normality as well.

Furthermore, both the model residuals plots above and the previously mentioned ACF plot for the differenced series reveal clear statistical significance at lag 16. This suggests our ARIMA model can probably be further improved with a specification of *q = 16*.

```
ts.arima.ma16 <- Arima(ts, order = c(3,1,16)) #  Fit and print out the revised ARIMA model
print(ts.arima.ma16)
checkresiduals(ts.arima.ma16) # Check the model residuals for normality and autocorrelations
```

![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-revised-model.png)


![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-revised-model-residuals.png)

As seen above, the ARIMA(3,1,16) model improves upon the previous ARIMA(3,1,2) model in that

1. the AIC for the revised model is smaller than that of the ARIMA(3,1,2) model;

2. the diagnostic plots this time look more like white noise with no significant autocorrelations present;

3. Ljung-Box test results for the revised model suggests non-significant model residuals, signaling that the model residuals are random and that the model provides an adequate fit to the data. 

Hence, we will go with the *ARIMA(3,1,16)* model for prediction.

## Predictions

Our model's predictions for the next 30 trading days are presented below.

```
library(astsa)
ts.prediction <- sarima.for(ts, n.ahead = 30, 3, 1, 16) %>% 
  print() # Generate our ARIMA model's 30-day predictions
```

![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-revised-model-predictions-numbers.png)


![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-revised-model-predictions-plot.png)

Are these predictions reliable?

We designate the past 30 trading days in our time series as the "hold-out" set, fit our chosen ARIMA model, and see how well the predictions fit the actual observed values.

```
ts.trun <- window(ts, end = time(tail(ts, n = 30)[1])) %>% 
  sarima.for(n.ahead = 30, 3, 1, 16) # Back test our ARIMA model
lines.default(ts)
```

![center](http://roywangtw.github.io/images/2017-12-07-ARIMA-revised-model-backtest-plot.png)

The red circles represent the predicted values for the past 30 trading days, forming a nearly straight line very quickly, which is odd given the series' predominantly oscillating pattern. 

Nonetheless, most of the actual observed values (i.e. the black line) do fall within the bounds of the 80% confidence levels (i.e. the dark grey shaded areas), hence lending our current model some degree of credibility. 

## Conclusions

This post presents a simple demonstration of using ARIMA modeling for predicting an ETF's price movements, and our model, at its current form, remains fairly naive. 

More refinements on the model might be obtained from segmenting out bull run periods from bear run periods for more sophisticated analysis. Further insights might also come from testing other forecasting models, such as the [ets models](https://ellisp.github.io/blog/2016/11/27/ets-friends), but those would be left for future exploration.

```
sessionInfo()
```

![center](http://roywangtw.github.io/images/2017-12-07-sessioninfo.png)
