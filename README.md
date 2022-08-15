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
- Rescaling: Min Max Scaler
- Encoding: One Hot Encoding, Target Encoding

## Feature Selection

I chose the top 7 features in terms of importance according to an Extra Trees model.

|Feature|Importance|
|-------|----------|
|vintage|0.272447|
|annual_premium|0.245530|
|age|0.164914|
|region_code|0.105027|
|vehicle_damage|0.069313|
|policy_sales_channel|0.059977|
|previously_insured|0.055369|

## Model Comparisson & Fine Tuning

|Model|Precision at 40%|Recall at 40%|
|-------|----------|----------|
Extra Trees|0.270304 +/- 0.000852|0.882177 +/- 0.002779|
Logistic Regression| 0.267552 +/-	0.000791|0.873196 +/-	0.002580|
KNN| 0.265781 +/- 0.001006| 0.867416 +/- 0.003284|

The model chosen was the Logistic regression because it runs approximately 4x faster than ExtraTrees, while having very close precision and recall numbers in comparison.

The method chosen to do the fine tuning was the Random Search, and below you have the hyperparemeters chosen for this project.

```
lr_model = lr(penalty = 'none',
                              solver = 'sag',
                              class_weight = 'balanced',
                              max_iter = 1000,
                              n_jobs=-1)
```


|Tuned Model|Precision at 40%|Recall at 40%|
|-------|----------|----------|
Logistic Regression| 0.268418 +/-	0.000684|0.876022 +/-	0.002231|

## Model Performance Visualization

The gain curve shows that by using the model to rank the clients, all of the interested clients are at the top ~%55 of the whole list.

![Gain Curve](https://img001.prntscr.com/file/img001/kZSJiFOURKK-lM-w_V8Sgg.png)

The lift curve shows that the model outperforms a random ordering by a rate of more than 2 for the top ~50% of the list.

![Lift Curve](https://img001.prntscr.com/file/img001/aYNh5YNgTlm5STZBzGQngg.png)

## Business Total Performance

The test dataset has 127,037 clients, assuming 3 minutes per call with each one of the clients, it would take 6,352 hours to call all of the clients.

According to [Indeed](https://www.indeed.com/career/call-center-representative/salaries), a call center representative gets paid $16.90 per hour.

By using the model, only the top 60% clients need to be called, which means a 40% reduction of hours worked that equate to $42,942.90

## Deployment
The model was deployed and can be requested thru API by a Google Sheets using a script I created. 

![12748784-5760-4110-b93a-34dd93876317](https://user-images.githubusercontent.com/102861289/184733476-e81abf82-70de-43b0-bd18-20ccf4f721c7.gif)

