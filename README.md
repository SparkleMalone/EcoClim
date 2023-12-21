# Data Basics (EcoClim)

### Learn the basics of manipulating data in R

In this workshop you will:

1. Download climate data from daymetr 
2. Format date elements
3. Manipulate data with tidyverse: 
+ Use select() to choose variables from a data frame.
+ Use filter() to choose data based on values.
+ Use mutate() to create new variables.
+ Use group_by() and summarize() to work with subsets of data.
+ Use full_join() to merge datasets
4. Write basic functions

### Load the required libraries
```{r, include=T}
library(daymetr)
library(tidyverse)
```

In this workshop we will explore climate data using climateR. 

```{r, include=T}
?getDaymet
```

```{r, include=T}
AOI <- aoi_get(country="USA")

Yale.Myers <- data.frame(longitude = -72.124395, latitude= 41.953219) 
Yale.Myers.sf <- st_as_sf( Yale.Myers, coords= c('longitude', 'latitude' ))

plot(AOI[1])
plot(Yale.Myers.sf, add=T, col='red')



Yale.Myers.daymet <- getDaymet( Yale.Myers.sf , varname= c( 'tmin', 'tmax', 'prcp'),
startDate= "1990-01-01",
endDate = "2022-12-31")
```
