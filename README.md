# Data Basics (EcoClim)
## Learn the basics of manipulating data


Load the required libraries
```{r, include=T}
library(climateR)
library(terra)
library(sf)
library(AOI)
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
