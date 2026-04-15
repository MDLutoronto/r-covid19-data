---
title: Importing Data
parent: COVID-19 data in R
layout: default
nav_order: 1
---

### **Importing Data**

You can download Covid-19 data from the John Hopkins Github data. We download the confirmed cases dataset, the deaths dataset and the recovered cases dataset. Note differences in the number of rows and columns.

```r
# IMPORT RAW DATA: Johns Hopkins Github data
confirmedraw <- read.csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv")
str(confirmedraw) # Check latest date at the end of data
deathsraw <- read.csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_deaths_global.csv")
recoveredraw <- read.csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_recovered_global.csv")
```