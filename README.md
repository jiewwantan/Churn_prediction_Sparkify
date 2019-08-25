# Churn Prediction Sparkify
## Overview

Predicting music streaming service user churn on local machine and AWS EMR.

User churn (cancellation) prediction is an imperative predictive tool. This project sets to solve this problem for a music streaming service: Sparkify. By exploring Sparkify usage data, the project identifies features for model learning. For computation efficiency reason, a tiny dataset (240Mb), a sample of the full dataset (12Gb) is used for initial data exploration, feature engineering and modelling experimentation on a local machine (Workflow in Sparkify_local.ipynb)

The initial work on the tiny dataset shall identify the most suitable model and hyper-parameters for the full dataset to train the final model . Once features and model are identified, they will be used for modelling the full dataset on AWS EMR.(Workflow in Sparkify_AWS_EMR.ipynb)

The actionable insight gained from churn prediction would be to identify users who are likely to churn and send them offers that hopefully will keep them from clicking cancellation confirmation.

My [Medium post](https://medium.com/@jiewwantan/sparkify-user-churn-prediction-using-pyspark-32be364e8296) provides a more detailed explanation of this project. 

## Requirements: 

1. Python 3
2. Pyspark
3. Pandas
4. Matplotlib
5. Seaborn
6. Jupyter notebook

## Instructions:

Data: 
[Tiny 240Mb](https://drive.google.com/open?id=1-hi73PWXdMxNLvYWJtL2Y6Rig2rT5B5K)
[Big 12Gb](s3a://udacity-dsnd/sparkify/sparkify_event_data.json)

1. To run Sparkify_local.ipynb:
    `python data/process_data.py data/disaster_messages.csv data/disaster_categories.csv data/DisasterResponse.db`
2. To run Sparkify_AWS_EMR.ipynb:
  Spin up an [AWS EMR](https://console.aws.amazon.com/elasticmapreduce/) cluster, create the Sparkify_AWS_EMR.ipynb notebook.
        
## Results

### Exploratory data analysis

[image1]: https://github.com/jiewwantan/Churn_prediction_Sparkify/blob/master/plots/churn_level.png "User Churn Status"
![User Churn Status][image1]

[image2]: https://github.com/jiewwantan/Churn_prediction_Sparkify/blob/master/plots/user_daily_churn.png "Daily evolution of User Churn Status"
![Daily evolution of User Churn Status][image2]

### Training results

[image3]: https://github.com/jiewwantan/Churn_prediction_Sparkify/blob/master/plots/feature_importance_GBTClassifier.png "Gradient Boosting Tree Classifier feature importance"
![Gradient Boosting Tree Classifier feature importance][image3]

All features are adopted for modelling the large dataset. 

### Test data evaluation results

On tiny data set on local machine:<br/>
`Evaluation result:<br/>
+---------+------+------+--------+
|precision|recall|    f1|accuracy|
+---------+------+------+--------+
|   0.8611|0.8662|0.8622|  0.8662|
+---------+------+------+--------+`

On large dataset on AWS: <br/>
`Evaluation result:<br />
+------+------+---------+--------+
|    f1|recall|precision|accuracy|
+------+------+---------+--------+
|0.7254|0.7868|   0.7444|  0.7908|
+------+------+---------+--------+`

