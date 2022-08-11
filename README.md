# Insurance cross-sell 

## Context of the project

A health insurance company wants to know which customers from their userbase are more likely to be interested by their new car insurance. That way, the company wouldn't need to contact their whole userbase, since that would take a lot of time, and consequently, money.

The company called a fraction of their clients to acquire informations regarding their vehicles and at the end asked if the person was interested in the car insurance or not.

## Solution planning

The planned solution was to create a machine learning model that can give a score to each client based on propensity to buy. That way, the callcenter workers could sort the score value from highest to lowest and start calling the top scoring clients. I will also give a estimation of when to stop calling the customers, based on the model metrics.

## Data Description
- Renaming columns
- Changing data types
- Statistic description of numerical (mean, median, std, skew, kurtosis) and categorical atributes

## Exploratory Data Analysis 

### Hypothesis List

1. Older people will be more interested.

__FALSE.__ The people that are more interested are around the median.

![](https://img001.prntscr.com/file/img001/MJ2fnd2kSqOgkZOS_eLogA.png)

2. People with a drivers license will be more interested.

__TRUE.__ People with a drivers license are more interested.

![](https://img001.prntscr.com/file/img001/ZwaD54ZgSV68z8dltBae8A.png)

3. People with lower annual premium are the most interested.

__TRUE.__ However, that only applies to the <10k range.

![](https://img001.prntscr.com/file/img001/FFkF2rfCSZWVCz5bBoTvlQ.png)

4. People with higher vehicle age will be more interested.

__TRUE.__ People with higher vehicle age are percentually more interested.

![](https://img001.prntscr.com/file/img001/4v5rlJVvSSmEL44F5UsA6A.png)


5. People that had their vehicle damaged will be more interested.

__TRUE.__ People with higher vehicle damage are percentually more interested.

![](https://img001.prntscr.com/file/img001/-JPedch9QZq36dwVd-sbbA.png)

## Data Preparation
## Feature Selection
## Model Comparisson & Fine Tuning
## Business Total Performance
## Model Performance Visualization
## Deployment
