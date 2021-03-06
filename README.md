## Rental listings Inquiries

The goal of this project is to predict the number of inquiries a new rental listing receives based on the listing�s creation date and other features. The number of inquiries for a particular listings are given to us in the form of "interest_level" feature. The project is based on a kaggle competition. The description of the competition can be found [here](https://www.kaggle.com/c/two-sigma-connect-rental-listing-inquiries). We will build a machine learning mode to predict the interest level for every listing with three categories, i.e, "low", "medium" and "high". This is a **multi-class classification** problem where we are suppose to predict probability of each class for every listing.

### Installation
- Clone this repo to your computer
- Change directory `cd NYC_rental_listings`
- Run `mkdir data` and download the csv data files from [here](https://www.kaggle.com/c/two-sigma-connect-rental-listing-inquiries/data) into this directory
- Install the requirements using `pip install -r requirements.txt` if moduels do not exist already
- Run python script: `python predict_apt_rfc.py` or `python predict_apt_xgb.py`

### Files
- **exploratory_analysis.ipynb** : A python nobebook for exploring the data and building features as necessary
- **predict_apt_rfc.py** : Script to perform prediction using the random forest classifier
- **prediction_apt_xgb** : Script to perform prediction using XGBoost module
- **predictions_rfc.csv** : Output file with predictions (RFC)
- **predictions_xgb.csv** : Output file with predictions (XGB)
- **README.md** : You are reading this file
- **requirements.txt** :  A text file of required python modules
- **data** : This is the data folder, not included here. The data can be downloaded from this [link](https://www.kaggle.com/c/two-sigma-connect-rental-listing-inquiries/data). A description of the data fields are also found there.

### Discussion/Summary
We built two models to predict customer interest level for every rental listing in the data provided by [2sigma/renthop](https://www.kaggle.com/c/two-sigma-connect-rental-listing-inquiries). The first model is based on Random Forest Classifier and the second one is using XGBoost package. The models are evaluated using a [multi-class log-loss](https://www.kaggle.com/c/two-sigma-connect-rental-listing-inquiries#evaluation) metric. A moderate amount of feature engineering was applied to the data before using them as input to the models. The following observations were made from our study:

- Random forest classifier gives a log-loss of 0.58066 on test set. Ideally, we want this to be as low as possible for accuracy of the prediction to be high. One can interpret this number in terms of predicted probability using this [plot](http://wiki.fast.ai/index.php/Log_Loss#Visualization). As we can see from the plot, above a predicted probability of 0.5 or so the log-loss decreases very gradually. A log-loss of 0.58 corresponds to more than 0.7 predicted probability, hence the accuracy of prediction. This model includes a new feature called "manager_skill" which was built using the given features.

- We also used XGBoost package to build a model and found a lower log loss of 0.5445 on an unseen test dataset (using Kaggle's public score board). Therefore XGBoost seems to give better prediction of probabilities for each class in this case. We have tweaked the parameters of the model and did a cross-validation to determine the best set of parameter that results in the lowest value of log-loss. We believe that the score can be improved further by making use of information on photos provided in the data, and a better treatment of high cardinality features such as 'manager_id' and 'building_id'. For example, [this](https://www.researchgate.net/publication/272522918_Including_High-Cardinality_Attributes_in_Predictive_Models_a_Case_Study_in_Churn_Prediction_in_the_Energy_Sector) paper describes a few interesting ways to handle high cardinality attributes.

We conclude that XGBoost gives more accurate predictions than random forest classifier. A log loss of 0.5445 was achieved using this model which corresponds to more than 0.75 predicted probability. The advantage of XGBoost is that it is faster to run and do not need any special treatment such as taking care of outliers or scaling features. The disadvantage is that it has lot of parameters that can be tweaked. 

The predictions of interest level for every new rental listing can be use by the rental company to better handle fraud control, identify potential listing quality issues, and allow owners and agents to better understand renter's needs and preferences.