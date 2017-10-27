# sa2geospatial
Recipe for SA2 geospatial mapping in Tableau

## Setup
1. Download SA2 Shapefiles from ABS:  
Statistical Area Level 2 (SA2) ASGS Ed 2016 Digital Boundaries in ESRI Shapefile Format
2. Prepare SA2 measures dataset:  
e.g. sa2_id|count_households|perc_churn|perc_churn_adjusted
3. Apply bayesian adjustment if appropriate:  
https://www.r-bloggers.com/understanding-empirical-bayes-estimation-using-baseball-statistics/
4. Connect to shapefiles, connect to measures, join on SA2_id
5. Create tableau data extract for better performance
6. Double click on Geometry measure to generate map

## Visualise measure
1. Colour by measure of interest

## Search for SA2
1. Create string parameters [SA2 Id Search] and [SA2 Name Search]; display parameters
2. Create field [Suburb Colour]; add as colour
```
IF 
    [SA2 Name Search] <> '' AND CONTAINS(LOWER([Sa2 Name16]),LOWER([SA2 Name Search])) 
THEN 
    1 
ELSEIF
    [SA2 Id Search] <> '' AND LOWER([Sa2 5Dig16]) = LOWER([SA2 Id Search])
THEN
    1
ELSE 
    0
END
```
3. Create field [Suburb Name]; add as label
```
IF 
    [SA2 Name Search] <> '' AND CONTAINS(LOWER([Sa2 Name16]),LOWER([SA2 Name Search])) 
THEN 
    [Sa2 Name16]
ELSEIF
    [SA2 Id Search] <> '' AND LOWER([Sa2 5Dig16]) = LOWER([SA2 Id Search])
THEN
    [Sa2 Name16]
END
```
