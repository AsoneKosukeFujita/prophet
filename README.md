# Example forecast of ferry load for one specified sailing and route
- If R not installed:
```
sudo apt-get -y install r-base
sudo apt-get -y install rstudio
R
```
- Prerequisites for installation of prophet package:
```
sudo apt-get update
sudo apt-get install liblapack-dev -y
sudo apt-get install liblapack3 -y
sudo apt-get install libopenblas-base -y
sudo apt-get install libopenblas-dev -y 
sudo apt-get install r-cran-rcpp r-cran-inline r-cran-rcpp
sudo apt-get install r-cran-rcppeigen
```
- Open RGui or RStudio in local directory C:/Users/aroug/Source/Repos/prophet/examples/
- Run historical ferry load data for specific sailing time and route
- Install prerequisites
```
install.packages("prophet")
install.packages("dplyr")
```
- Run learning routine
```
library(prophet)
library(dplyr)
m <- prophet(df)
df <- read.csv('C:/Users/aroug/Source/Repos/prophet/examples/temp0620.csv') %>% mutate(y=log(y))
```
- View learning data frame
```
m
df
```
- View selections of learning data frame
```
class(df$ds)
class(df$y)
head(df$y)
head(df$ds)
tail(df$y)
tail(df$ds)
```
- Forecast loads with seasonality of 7 days, then transform result to ```exp(y)```
```
future <- make_future_dataframe(m, periods = 7)
tail(future)
forecast <- predict(m, future)
```
- View the output data frame
```
future
forecast
tail(forecast[c('ds', 'yhat', 'yhat_lower', 'yhat_upper')])
```
- Plot the (natural logarithm of) results
```
plot(m, forecast)
prophet_plot_components(m, forecast)
```
- See more information on data frame ```forecast```
```
str(forecast)
tail(forecast)
head(forecast)
names(forecast)
dim(forecast) # no of rows and cols
```
- Investigate the specific values of the (log of) forecast load ```yhat```
```
forecast$yhat
```
- Calculate the load % forecast by exponentiating the above values
```
exp(forecast$yhat)
```
- Create a new data frame with only the future dates and forecast of load %
```
df1 <- data.frame(forecast$ds,exp(forecast$yhat))
df1
plot(df1,type="o", xlab = "Weekly Seasonality", ylab = "Load %",main = "Forecast of Load % for Daily Sailing at 0620")
```
