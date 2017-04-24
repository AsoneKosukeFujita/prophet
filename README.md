# Run example forecast of ferry load for one specified sailing and route
- open RGui or RStudio in local directory C:/Users/aroug/Source/Repos/prophet/examples/
- run historical ferry loading data for specific sailing time and route
- install prerequisites
```
install.packages("prophet")
install.packages("dplyr")
```
- run learning routine
```
library(prophet)
library(dplyr)
m <- prophet(df)
df <- read.csv('C:/Users/aroug/Source/Repos/prophet/examples/temp0620.csv') %>% mutate(y=log(y))
```
- view learning data
```
m
df
```
- Selections of learning data
```
class(df$ds)
class(df$y)
head(df$y)
head(df$ds)
tail(df$y)
tail(df$ds)
```
- create forecast: to forecast loading then transform result to ```exp(y)```
```
future <- make_future_dataframe(m, periods = 7)
tail(future)
forecast <- predict(m, future)
```
View the output data
```
future
forecast
tail(forecast[c('ds', 'yhat', 'yhat_lower', 'yhat_upper')])
```
- plot the (natural logarithm of) results
```
plot(m, forecast)
prophet_plot_components(m, forecast)
```
