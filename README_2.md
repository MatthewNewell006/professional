# HIV Forecasting (Case Study #02)

![info](forecast_HIV_infections/image/hiv_intro.jpeg)

## Overview

Due to the development of anti-retroviral therapies the HIV/AIDS epidemic is generally considered to be under control in the US. However, as of 2015 there were 971,524 people living with diagnosed HIV in the US with an estimation of 37,600 new HIV diagnoses in 2014. HIV infection rates continue to be particularly problematic in communities of color, among men who have sex with men (MSM), the transgender community, and other vulnerable populations in the US. Socioeconomic factors are a significant risk factor for HIV infection and likely contribute to HIV infection risk in these communities. The current US opioid crisis has further complicated the efforts to combat HIV with HIV infection outbreaks now hitting regions that weren’t previously thought to be vulnerable to such outbreaks.

## Objective

- Build a linear regression model that utilizies the HIV infection data, census data, data on the opioid crisis, and data on sexual orientation
- Find useful insights as to predicting HIV infection rates of different states

## Contents

1. [Dataset](#Dataset)
2. [Questions](#Questions)
3. [Exploration](#Exploration)
4. [Analysis](#Analysis)
5. [Geography](#Geography)
6. [Summary](#Summary)

# Dataset

The original data set using `merge_data.ipynb` to explore `opoid_df` shows the AMFAR Opoid and HIV Data with the County code. The dataframe has **744,686 rows and 9 columns.**

![data](forecast_HIV_infections/image/clean_data.png)

# Questions

- How do socioeconomic factors from census data affect HIV infection rates?
- How do factors like drug abuse such as opioid crisis affect the HIV infection rates?
- Which states have the highest HIV infection rates?

# Exploration

The dataset we used was a compilation from three larger datasets, and created through Eric Louge's program to merge them. Our smaller set contains 3140 entries and 38 columns which was taken only from 2015. 

We are doing a Groupby: STATEABBREVIATION

And dropping these columns. [Unnamed: 0,Unnamed: 0.1, drugdeathrate,drugdeathrate_est]
drugdeathrate and drugdeathrate_est are are similar to drugdeath

And summing these columns ["HIVdiagnoses","PLHIV,Population","drugdeaths,num_SSPs,bup_phys,ADULTMEN,MSM12MTH,MSM5YEAR,fac]

And averageing these columns ["HIVincidence","HIVprevalence", "mme_percap","partD30dayrxrate","pctunins","drugdep","pctunmetneed","nonmedpain","%msm12month","%msm5yr","unemployment_rate","poverty_rate","household_income"]

## Exploratory Data Analysis

# Analysis
In order to find the best fitting model we tested four different types of models to apply to our data. Those models were a KNNregressor, with varying amounts of neighbors, and three types of linear regressor including LASSO, ridge, and elasticnet. In order to create these models we seperated the large set of data with an 80/20 train test split. Then with the larger training data we used KFold validation to find which of these models would best approximate our data.  

## By Socioeconomic Factors
### Income and Deaths
![income deaths](forecast_HIV_infections/image/plot/income_deaths.png)

## By State

### California

![scatter1](forecast_HIV_infections/image/scatters/CA.png)


### Florida

![scatter2](forecast_HIV_infections/image/scatters/FL.png)

### New York

![scatter3](forecast_HIV_infections/image/scatters/NY.png)

### Texas

![scatter4](forecast_HIV_infections/image/scatters/CA.png)



## Scores
|Model_Type|Variables        |Neighbors|Score            |
|----------|-----------------|-----|------------------|
|CA        |KNN              |3    |9.214740560062076 |
|CA        |KNN              |4    |8.715017704261896 |
|CA        |KNN              |5    |8.413587286365217 |
|CA        |KNN              |6    |8.846789193345963 |
|CA        |KNN              |7    |9.19012159545916  |
|CA        |Linear Regression|     |16.911087735249893|
|CA        |Ridge            |     |33.82436244321132 |
|CA        |Lasso            |     |49.62575306196318 |
|CA        |Elastic Net      |     |65.68968835523484 |
|TX        |KNN              |3    |29.556401420467225|
|TX        |KNN              |4    |29.15512249814647 |
|TX        |KNN              |5    |27.824888861091523|
|TX        |KNN              |6    |27.48645140199711 |
|TX        |KNN              |7    |26.881981728132523|
|TX        |Linear Regression|     |29.101851636352166|
|TX        |Ridge            |     |58.125112053949714|
|TX        |Lasso            |     |87.53003284351831 |
|TX        |Elastic Net      |     |117.00809091119318|
|FL        |KNN              |3    |40.84064363286674 |
|FL        |KNN              |4    |40.56504473370582 |
|FL        |KNN              |5    |41.64745635139665 |
|FL        |KNN              |6    |44.08629982025825 |
|FL        |KNN              |7    |43.047496745454445|
|FL        |Linear Regression|     |45.096643181329576|
|FL        |Ridge            |     |86.028884917778   |
|FL        |Lasso            |     |120.34808305692113|
|FL        |Elastic Net      |     |155.96354311934908|
|NY        |KNN              |3    |17.905096569367164|
|NY        |KNN              |4    |18.556585703090416|
|NY        |KNN              |5    |18.94779197992034 |
|NY        |KNN              |6    |18.766839666660374|
|NY        |KNN              |7    |18.95486849972667 |
|NY        |Linear Regression|     |32.18859276985525 |
|NY        |Ridge            |     |55.60482352931254 |
|NY        |Lasso            |     |71.78798465369255 |
|NY        |Elastic Net      |     |87.4909520389656  |

![scatter4](forecast_HIV_infections/image/our_models.png)

# Summary
    Our analysis showed that the elastic net model consistently produced the best model to predict future incidence rates of HIV.  An interesting observation to note is that in our KNN models, as the number of neighbors increased, the score of the model went down which was unexpected.  


