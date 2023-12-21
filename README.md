# Data Basics (EcoClim)
Learn the basics of manipulating data

library(climateR)
library(terra)
library(sf)
library(AOI)

?getDaymet

AOI <- aoi_get(country="USA")

Yale.Myers <- data.frame(longitude = -72.124395, latitude= 41.953219) 
Yale.Myers.sf <- st_as_sf( Yale.Myers, coords= c('longitude', 'latitude' ))

plot(AOI[1])
plot(Yale.Myers.sf, add=T, col='red')



Yale.Myers.daymet <- getDaymet( Yale.Myers.sf ,
varname= c( 'tmin', 'tmax', 'prcp'),
startDate= "1990-01-01",
endDate = "2022-12-31")

