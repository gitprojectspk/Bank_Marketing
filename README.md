# Bank Marketing (Campaign)
![image](https://user-images.githubusercontent.com/96436449/195425543-cab08353-4291-4432-8ee9-95f0f8e9b9e3.png)
# Problem Statement:
![image](https://user-images.githubusercontent.com/96436449/195426088-893a9cc1-80a7-43ed-83a6-d791af5d32fa.png)
# Dataset Information

https://archive.ics.uci.edu/ml/datasets/Bank+Marketing/
Csv file : bank-additional-full.csv

![image](https://user-images.githubusercontent.com/96436449/195436179-25390688-a84e-4673-83b2-436c791f91bc.png)

- There are 10 numeric columns and 11 Categorical Columns
- No missing data found.
- 12 duplicate rows found.

# Exploratory Data Analysis – Univariate Analysis

![image](https://user-images.githubusercontent.com/96436449/195436455-4a82e2f0-0c22-495b-9b2b-5e1cdcdff963.png)

- Most of the clients are working as admin 25% and blue collar 22% job category.
- 60% of the clients are married.
- Most of the clients 29% hold University degree.
- The no of clients who defaulted on a credit, are very less. It shows 80% data for 'No'. % of yes is almost 0. so this feature doesn’t seem to be very for prediction purposes and can be dropped from the dataset.
- Housing Shows almost equal % of yes and no.
- Most of the clients do not have personal loan.

# Exploratory Data Analysis – Categorical Features
![image](https://user-images.githubusercontent.com/96436449/195436736-593ee3cf-8909-49cb-b884-e413f59bd630.png)
-More than 63% of all clients were contacted through cellular phone.
-Most of the clients were contacted in the month of May 33%.
-Here we see equal distribution of the data in the graph and the % amongst the days. So, there is no significant day which shows more activity than others.
-More than 86% of clients were never covered by previous marketing campaigns. 
-We see there is imbalance in data. only 11.70% clients have subscribed to a term deposit.

# Exploratory Data Analysis – Numerical Features
![image](https://user-images.githubusercontent.com/96436449/195436865-4771d45d-1bf9-4634-9d8a-17292a4526c6.png)

- The graph of age shows normal distribution.
- The graph of pdays, previous, duration, campaign shows skewness. 
pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted).
- pdays columns shows above 96% values are having 999 value. So, this column should be removed.
- The variable “duration” will need to be dropped before we start building a predictive model because it highly affects the output target (e.g., if duration=0 then y=”no”). Yet, the duration is not known before a call is performed.
- Other graphs shows several spikes in the data.

# Exploratory Data Analysis – Bivariate Analysis
![image](https://user-images.githubusercontent.com/96436449/195436978-7aaf5246-b8cf-4e30-9dd7-88f8e5cceb3d.png)

The % of clients showing interest in 'term deposit' is more when they are married, holds university degree and no defaulted to credit.
The retired people seem to have higher % of 'Yes' for term deposit than other job category clients.
The clients having housing, loan have higher % or saying no to term deposit.
The months may, jun, juy, aug shows more clients responding to term deposit
If poutcome = success then the % of 'yes' to term deposit is high
% of interest in 'Deposit’ is more when clients are contacted via cellular mode.
Clients having longer durations shows more interest in term deposit

![image](https://user-images.githubusercontent.com/96436449/195437037-e360569e-61ff-4c7c-876e-afb4d93fd57d.png)

- The features like age, pdays, duration, campaign, duration has some outliers

![image](https://user-images.githubusercontent.com/96436449/195437064-410e1d15-7c84-4c7d-a933-e209d7ac18df.png)

As we see in above graph , euribor3m is highly corelated with 'emp_var_rate' and nr_employed. So, I dropped 'emp_var_rate' and nr_employed as they will only add redundancy and overfitting.

![image](https://user-images.githubusercontent.com/96436449/195437143-074e8dc7-3476-44fa-b312-9bbbf3b7cbf0.png)


# Data Pre-Processing
- Here, I dropped the unwanted features, handled missing data, removed outliers.
- Before feeding the data to model, I converted the categorical column into a numerical one using One-Hot-Encoding
- The dataset has been separated in a Train dataset (31392 samples) and a Test dataset (7849 samples). 
- The data was scaled before feeding into the respective models.

# Model Selection
For all the models under study, to avoid over-fitting, I optimized the corresponding hyper-parameters by a 5-fold cross-validation on the Train set. I then evaluated on the Test set the models trained on the entire Train set.
- Random Forest shows better accuracy and F1 score

![image](https://user-images.githubusercontent.com/96436449/195437539-87e9df10-4027-4ec3-8a3d-7014d9c484d0.png)

# Imbalance Data Handling

There is lot of imbalance amongst the subscribe class 
No     35323
Yes       3918
Oversampling is one of the most widely used techniques to deal with imbalance classes. Using RandomOverSampler method, and class weight adjusted to balanced , f1 score improved to 92.03 and Accuracy increased to 92.11

# Hyper Parameter Tunning
Using GridSearchCV, the hyperparameters are selected, using which the accuracy changed to 84.39 with F1 score : 86.86

Using RandomizedSearchCV, the hyperparameters are selected, using which the accuracy increased to 91.88 with F1 score : 91.73

roc_auc score is also good 0.76

Feature Importance
Feature importance shows Duration , Euribor3m  and Age as the important features.
![image](https://user-images.githubusercontent.com/96436449/195437781-14c6ba94-84e6-4aee-a89f-c5ba2e76ef65.png)

As the problem states, Duration feature is not recommended as this will be difficult to explain the result to business and it will
be difficult for business to campaign based on duration. After removing duration feature, model accuracy changed to 88.95 and F1 sore is 88.56. which is still good. 
Feature importance shows Euribor3m and Age as the important features.
![image](https://user-images.githubusercontent.com/96436449/195437923-cfb793d3-12e7-4d3f-a35a-8251a8d9c7ca.png)
