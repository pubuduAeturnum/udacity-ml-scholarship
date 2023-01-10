# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Pubudu De Alwis

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
When I tried to submit my predictions to keggle I relize that keggle was not there as a command in the current sagemaker project therefore I had to install keggle using pip -U install kaggle and then create a symbolic link to /usr/bin/kaggle using /root/.local/bin/kaggle.
To submit a result in to kaggle using predictor we need to predict the count using test.csv dataset by using *predictor.predict(test)*

### What was the top ranked model that performed?
WeightedEnsemble_L3

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
With the use of Sagemaker Data wrangler EDA is done and found that using Featurized Date/Time transformation we can further devide the datetime field into year, month and date to add these features to do current dataframe first the datetime field in the dataframe is converted into pandas datetime fromat and then extract the year, month and day values using dt.
```
train["year"] = train["datetime"].dt.year
train["month"] = train["datetime"].dt.month
train["day"] = train["datetime"].dt.day
train["dayofweek"] = train["datetime"].dt.dayofweek
train["temp__sum_values"] = temp_sum_values_train["temp__sum_values"]
test["year"] = test["datetime"].dt.year
test["month"] = test["datetime"].dt.month
test["day"] = test["datetime"].dt.day
test["dayofweek"] = test["datetime"].dt.dayofweek
test["temp__sum_values"] = temp_sum_values_test["temp__sum_values"]
```

### How much better did your model preform after adding additional features and why do you think that is?
When add the new features to the dataset the root mean squared value is increased from 52.845193 to 52.907886. Therefore, model performance has been reduced to some level with the test dataset but with hyperparameter tunning it was able to reduced to 52.588371.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
Model start to perform well after hyperparameters are added to the training by increasing the kaggle score values.

### If you were given more time with this dataset, where do you think you would spend more time?
Do to the exploratary data analysis to get more insight about the provided dataset and improve it by catergorizing  data and adding more features using current features.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|net_bag_folds|net_bag_sets|net_stack_levels|score|
|--|--|--|--|--|
|initial|0|1|0|1.80562|
|add_features|0|1|0|1.75632|
|hpo|0|20|0|1.86412|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](img/model_test_score.png)

## Summary

With the use of autogluon we can train different ML algorithms and then we are able to get the best perform ML algorithm for the training dataset which reduce lot of workload that MLE spend when selecting an best ML algorithms to train their dataset which provide better performance. In this project bike sharing demand kaggle competetion has been done using the autogluon with inital row dataset, adding new features and then modifying hyperparameters of the autogluon and able to achieve kaggle scores as follow;
* Initial - 1.79267
* Add_features - 1.75515
* Modifying hyperparameters - 1.86412
With modifying hyperparameters with adding new features the Kaggle score has significant improvement.