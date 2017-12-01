---
title: "R Notebook"
output: html_notebook
---

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code. 

Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Ctrl+Shift+Enter*. 

```{r}
library(prophet)
library(dplyr)
```

```{r}
m <- prophet(df)
df <- read.csv('/home/alastair/source/prophet/examples/temp0620.csv') %>% mutate(y=log(y))
```
  
  
```{r}
future <- make_future_dataframe(m, periods = 7)
tail(future)
```

```{r}
forecast <- predict(m, future)
```

```{r}
plot(m, forecast)
```

```{r}
prophet_plot_components(m, forecast)
```

```{r}
df1 <- data.frame(forecast$ds,exp(forecast$yhat))
```

```{r}
plot(df1,type="o", xlab = "Weekly Seasonality", ylab = "Load %",main = "Forecast of Load % for Daily Sailing at 0620")
```


Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Ctrl+Alt+I*.

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Ctrl+Shift+K* to preview the HTML file).

The preview shows you a rendered HTML copy of the contents of the editor. Consequently, unlike *Knit*, *Preview* does not run any R code chunks. Instead, the output of the chunk when it was last run in the editor is displayed.
