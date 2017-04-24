# Run example forecast of ferry load for one specified sailing and route
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
- Create forecast loads then transform result to ```exp(y)```
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
