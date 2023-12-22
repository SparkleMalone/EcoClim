# Data Basics (EcoClim)

### Learn the basics of manipulating data in R

In this workshop you will:

1. Download climate data with daymetr 
2. Format date elements
3. Manipulate data with tidyverse: 
    + Use select() to choose variables from a data frame.
    + Use filter() to choose data based on values.
    + Use mutate() to create new variables.
    + Use group_by() and summarize() to work with subsets of data.
    + Use full_join() to merge datasets
4. Write basic functions
5. Visualize data with ggplot2

### Load the required libraries
```{r, include=T}
library(daymetr)
library(tidyverse)
```
## What is the climate of Yale-Myers Forest?

Yale-Myers Forest is a 7,840 acre research forest Connecticut. It is a hub for education, research, and harvesting operations within the Yale School Forest System. The forest primarily consists of mixed hardwoods on glacial till soils, featuring a significant presence of hemlock, scattered white pine stands from old field origins, and red pine plantations established in the 1940s. 

To explore the climate of the area, download daily daymet data for (41.952909, -72.123859). Review the arguments for the download_daymet() function.
```{r, include=T}
?download_daymet()
```
To use the download_daymet() function you need the latitude, longitude, start (1990), and end (2018). 

```{r, include=T}
Yale.Myers.daymet <- download_daymet( lat =  41.952909,
                                      lon = -72.123859,
                                      start = 1990,
                                      end = 2018)
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
