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

You now have a nested list that includes information on the site location etc. The true climate data is stored in the "data" part of the nested list. Pull the data out of the list and create a dataframe.

```{r, include=T}
Yale.Myers <- as.data.frame(Yale.Myers.daymet$data)
```
Look at the dataframe:
```{r, include=T}
head(Yale.Myers )
```
Evaluate the data types:
```{r, include=T}
summary( Yale.Myers)
```
Format the time variables and create a date in the format YYYY-mm-dd :
```{r, include=T}
Yale.Myers$year.day <- paste( Yale.Myers$year, Yale.Myers$yday, sep="-") %>% as.Date(format="%Y-%j")
```
```{r, include=F, ecoh=F}
head( Yale.Myers)
```

Yale.Myers$date <-format( Yale.Myers$year.day, "%Y-%m-%d")%>%  as.Date()
class(Yale.Myers$date)

Yale.Myers <-Yale.Myers %>% mutate(month = format(Yale.Myers$date, format="%m"),
                     julianD = format(Yale.Myers$date, format="%j") )

# With Daymet data you have to calculate the mean temperature:

Yale.Myers$tmean = (0.606 *as.numeric(Yale.Myers$tmax..deg.c.)) + 0.394 * as.numeric(Yale.Myers$tmin..deg.c.)

summary(Yale.Myers$tmean)

# Rename columns:
Yale.Myers.rn <-Yale.Myers %>% mutate(tmax=tmax..deg.c., tmin=tmin..deg.c., prcp = prcp..mm.day.)

head(Yale.Myers.rn )

# Subset the dataset to include only [date, month, year, julianD, tmax..deg.c., tmin..deg.c., tmean, and prcp..mm.day.] :

Yale.Myers.sub <-Yale.Myers.rn %>% select(date, month, year, julianD, tmax, tmin, tmean, prcp)
head(Yale.Myers.sub )

# Create Annual and monthly summaries of conditions
Yale.Myers.annual <-Yale.Myers.sub %>% group_by(year) %>% summarise( tmax = max(tmax), tmin = min(tmin), tmean = mean(tmean), prcp = sum(prcp))

head(Yale.Myers.annual)
  
Yale.Myers.monthly <-Yale.Myers.sub %>% group_by(month) %>% summarise( tmax = max(tmax), tmin = min(tmin), tmean = mean(tmean), prcp = sum(prcp))

head(Yale.Myers.monthly)

Yale.Myers.yearmon <-Yale.Myers.sub %>% group_by(month, year) %>% summarise( tmax = max(tmax), tmin = min(tmin), tmean = mean(tmean), prcp = sum(prcp))

head(Yale.Myers.yearmon )

# Subset mean annual temperate and year. Then rename tmean with "Yale-Myers"

Yale.Myers.annual.tmean <- Yale.Myers.annual %>% mutate(Yale.Myers = tmean) %>% select(year, Yale.Myers)

head(Yale.Myers.annual.tmean)


# Find a location of interest within the USA in google earth (https://earth.google.com/) and record the latitude and longitude in decimal degrees. Next, download Daymet data for that location. Join your location information with Yale.Myers.annual.tmean in a dataframe called climateCompare:

YS.daymet <- download_daymet( lat =  44.434933,
                                      lon = -110.595371,
                                      start = 1990,
                                      end = 2018)

# ....

save(Yale.Myers, Yale.Myers.sub, file="EcoClim_out.RDATA" )

