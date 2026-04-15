---
title: Data Cleaning
parent: COVID-19 data in R
layout: default
nav_order: 2
---

### **Data Cleaning**

The next step is the data cleaning process. We want to create country level and global combined datasets with one row per country per date. To do this, we can to convert each dataset from wide format to long format and aggregate at the country level. The cleaned datasets are called confirmed, deaths and recovered. We also combine all three time series datasets into a new time series dataset called country.

```r
# DATA CLEANING
library(tidyr)
library(dplyr)

confirmed <- confirmedraw %>% gather(key="date", value="confirmed", -c(Country.Region, Province.State, Lat, Long)) %>% group_by(Country.Region, date) %>% summarize(confirmed=sum(confirmed))
deaths <- deathsraw %>% gather(key="date", value="deaths", -c(Country.Region, Province.State, Lat, Long)) %>% group_by(Country.Region, date) %>% summarize(deaths=sum(deaths))
recovered <- recoveredraw %>% gather(key="date", value="recovered", -c(Country.Region, Province.State, Lat, Long)) %>% group_by(Country.Region, date) %>% summarize(recovered=sum(recovered))

summary(confirmed)
```

```r
# Final data: combine all three
country <- full_join(confirmed, deaths) %>% full_join(recovered)
```
 

We fix the date variable. We create two new variables: the cumulative number of confirmed cases and the number of days variables. We create an aggregate country-level dataset called world.

```r
# Date variable
# Fix date variable and convert from character to date
str(country) # check date character
country$date <- country$date %>% sub("X", "", .) %>% as.Date("%m.%d.%y")
str(country) # check date Date
# Create new variable: number of days
country <- country %>% group_by(Country.Region) %>% mutate(cumconfirmed=cumsum(confirmed), days = date - first(date) + 1)
```

```r
# Aggregate at world level
world <- country %>% group_by(date) %>% summarize(confirmed=sum(confirmed), cumconfirmed=sum(cumconfirmed), deaths=sum(deaths), recovered=sum(recovered)) %>% mutate(days = date - first(date) + 1)
```
 

We can extract specific countries from the combined country dataset. We extract Italy here.

```r
# Extract specific country: Italy 
italy <- country %>% filter(Country.Region=="Italy")
```