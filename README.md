# EcoClim

EcoClim is a collection of functions used to calculate annual climatic variables used in ecological evaluations.  Variable calculation requires complete daily climate data for entire years.  

Functions and definitions of annual climatic variables used in ecological evaluations. Climate variable layers were developed by Rehfeldt et al. 2006 <https://www.fs.usda.gov/rm/pubs_other/rmrs_2006_rehfeldt_g001.pdf>. 

## Temperature
- D100 :   The sum of degree-days (Julian Date) > 5  ̊C 
- DD0  :   The sum of days > 0 ̊C 
- DD5  :   The sum of days > 5 ̊C
- FDAY :   First freeze day (Julian Date)
- MAT  :   Mean Annual Temperature ( ̊C)
- FFP  :   Length of frost free period (days)
- MMAX :   Mean Maximum Temperature ( ̊C)
- MTCM :   Mean temperature in coldest month ( ̊C)
- MTWM :   Mean temperature in warmest month ( ̊C)
- MMIN :   Mean minimum temperature in coldest month ( ̊C) 
- MINDD0:  Negative degree-days using minimum daily temperature for calculation (days)
- SDAY :   Date (Julian Date) of last freezing temperature in spring 
- FDAY : Date (Julian Date) of first freezing temperature in autumn
- GSDD5 : Mean degree-days > 5 ̊C between SDAY and FDAY. MMAX Mean temperature in warmest
month (days)
- TDIFF : Summer–winter temperature differential: MTWM-MTCM MAPDD5 (MAP X DD5)/1000 ( ̊C)

##  PRECIPITATION
- MAP : Mean annual precipitation (mm)
- GSP : April–September precipitation (mm)
- SMRP : Summer Precipitation: July–August precipitation (mm)
- SPRP : Spring Precipitation: April–May precipitation (mm)
- WINP : Winter Precipitation: November–February precipitation (mm)
- PRATIO : Growing season precipitation balance: GSP/MAP (mm)
- SMRPB : Summer Precipitation Balance: (jul + aug+sep)/(apr +may+jun) (mm)
- SMRSPRPB : Summer/Spring precipitation balance: (jul+aug)/(apr+may) (mm)
- SDI : Summer dryness index: (GSDD5)0.5/gsp
- SDIMINDD0 : SDI x MINDD0
- TDGSP : TDIFF/GSP ( ̊C / mm)
- MAPDD5: (MAP x MINDD0) / 1000