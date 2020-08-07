# Case Study - Churn Prediction

<p align="center">
<img src = "https://github.com/brentthayer1/supervised-learning-case-study/blob/master/img/header.jpg" class = "center" width = "300" height = "200"/>
</p>

## Overview

A ride-sharing company (Company X) is interested in predicting rider retention.
To help explore this question, a sample dataset of a cohort of
users who signed up for an account in January 2014 was used. The data was pulled on July
1, 2014. Users are condidered retained if they were “active” (i.e. took a trip)
in the preceding 30 days (from the day the data was pulled). In other words, a
user is "active" if they have taken a trip since June 1, 2014. 

## Contents

1. [Dataset](#Dataset)
2. [Questions](#Questions)
3. [Exploration](#Exploration)
4. [Summary](#Summary)

# Dataset

The original data set was churn.csv and was split into 3 datasets with subsequent train and test


# Questions

- How many users are considered active.
- What factors contribute to rider retention.
- What can be be done to solidify active status

# Exploration

Using a subset of our sample data, train data, we began with determining which columns we found to be crucial to our process.
Namely, those columns that were crucial to factoring out which users were active / inactive. The columns we worked with were "Last Trip",
"Trips Within 30 Days", and "Signup". Considering the "Signup" column made sense consdiering that if a user became active within 30 days
of our data pull, it would effect our model negatively. The data needs to reflect established users to better confirm predictive outcomes.
A mask was then implemented to offer a divide between active and inacitve for further testing.

The dates for "Last Trip" and "Signup", were converted to Date Time objects to allow us to perform further operations.

Boolean values in columns of "Active" users and "Luxury Car Users" were converted to integer datatypes of 0's and 1's for summation and further analysis.

"NaN" values were found in "Average Rating by Driver", "Average Rating of Driver", and "Phone". These were replaced with values that wouldn't have a negative effect on our model. The former two columns with "NaN" values, had those values replaced with the mean of the values in their respective columns. However The later column, "Phone", was replaced with "Unknown".

<img src = "https://github.com/brentthayer1/supervised-learning-case-study/blob/master/img/eda_stuff.png" class = "center" width = "500" height = "400"/>


<p align="left">
<img src = "https://github.com/brentthayer1/supervised-learning-case-study/blob/master/img/Screen%20Shot%202020-08-07%20at%205.00.29%20PM.png" class = "center"/>
</p>


## Exploratory Data Analysis

We put RandomForests and GradientBoost through a grid search. First we searched through max depth and max features. After we found optimal results for those we searched for the optimal number of estimators. We found 200 estimators, Sqrt of the features, and a depth of 6 to be optimal for both.

We found that the estimators for GridSearch and Gradient Booster were both 200."
Should be 'randomforest' and gradientbooster

<br><br>

<p align="center">
<img src = "https://github.com/brentthayer1/supervised-learning-case-study/blob/master/img/Screen%20Shot%202020-08-07%20at%204.51.36%20PM.png" class = "center"/>
</p>

<br><br>

<table>
  <tr>
    <td>Gradient Boosting</td>
    <td>Random Forest</td>
    <td>Reciever Operating Characterisitc</td>
  </tr>
  <tr>
    <td><img src="https://github.com/brentthayer1/supervised-learning-case-study/blob/master/img/grad_boost_feature_importances.png" width = "500" height = "300"></td>
    <td><img src="https://github.com/brentthayer1/supervised-learning-case-study/blob/master/img/rand_forest_feat_importances.png" width = "500" height = "300"></td>
    <td><img src="https://github.com/brentthayer1/supervised-learning-case-study/blob/master/img/roc_curves.png" width = "500" height = "300"></td>
  </tr>
 </table>



## Summary

Initially we found the performace for both train and test data were similar. We questioned  whether or not there could be leakage. Doing a split / train on our data, dropping different features, we found that there was no difference in performance in train / test data. We concluded that there wa no leakage.
