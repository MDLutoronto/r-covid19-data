---
title: Summary Statistics
parent: COVID-19 data in R
layout: default
nav_order: 3
---

### **Summary Statistics**
{: #summary-statistics}

We can obtain useful summary statistics from our final cleaned datasets country and world using the summary function and using the by function with the summary function.

```r
# Summary Statistics
summary(country)
by(country$confirmed, country$Country.Region, summary
by(country$cumconfirmed, country$Country.Region, summary)
by(country$deaths, country$Country.Region, summary)
by(country$recovered, country$Country.Region, summary)
summary(world)
summary(italy)
```