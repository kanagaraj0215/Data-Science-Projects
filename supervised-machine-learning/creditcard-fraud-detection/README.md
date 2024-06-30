## Credit Card Fraud Detection

**Credit Card Fraud:** <br />
A credit card fraudulent transaction is an unauthorized transaction made using a credit card without the cardholder's knowledge or consent. These transactions are typically carried out by individuals or groups engaged in illegal activities to steal money or obtain goods and services. There are many types of credit card fraudulent transactions, such as card-present fraud, card-not-present fraud, skimming, phishing, etc.

**Objective:** <br />
This project aims to develop a machine-learning model to detect fraudulent credit card transactions. This is achieved by analyzing transaction data to identify patterns that distinguish fraud activities from legitimate ones. 

**Data Source:** <br />
The dataset is extracted from the open-source website Kaggle. The dataset simulated credit card transactions from 1st Jan 2019 to 31st Dec 2020.

**Data Preprocessing:** <br />

- The dataset contained 555,719 observations and 23 fields. The column 'Unnamed: 0' is a unique identifier of the observation. It doesn't provide additional value, so the field has been dropped. 
- Any features with a correlation value >0.95 are considered significantly correlated. Highly correlated features create multicollinearity, making it difficult to determine the individual effect of each independent variable on the dependent variable. Two features are highly correlated, and those features are dropped from the data set.
- The dataset contains no missing values and no duplicate observations. The dataset didn't have any duplicates or null attributes. 
- New feature age is extracted using dob and transaction time. New features' hours and days are selected from transaction date time after extraction features dob and transaction date time are removed from the dataset. 
- Column merchants, first and last names, and streets are not helpful. These features are dropped from the dataset. 

**Exploratory Data Analysis (EDA):** <br />

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/Histogram_of_Amount.png" width="750" height="500"/>
</p>

- The higher amount misinterprets the histogram. Hence, the 0.99 quantile was used to remove the noise. The histogram shows that the data is skewed right.

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/box_plot_transaction_amount_fraud_flag.png" width="750" height="500"/>
</p>

- The box plot to have been used visualize the distribution of transaction amounts by fraud status. It is interesting to note that all fraudulent transactions are low-value transactions(less than 150).

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/scatter_plot_transaction_amount_vs_city_fraud_flag.png" width="750" height="500"/>
</p>

- The scatter plot have been used to visualize the transaction amount vs city population by fraud status. It shows a weak correlation for both fraudulent and non-fraudulent transactions.

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/Distribution_of_Categories_by_Fraud.png" width="750" height="500"/>
</p>

- It is interesting to note most of the fraud happened in the categories shopping_POS, shopping_net, misc_net, grocery_pos, and gas_transport

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/Hourly_Distribution_of_Fraudulent_Transactions.png" width="750" height="500"/>
</p>

- It is interesting to note that most fraudulent transactions happened between 10 PM and 3 AM at night.


<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/Age_Distribution_of_Fraudulent_Transactions.png" width="750" height="500"/>
</p>

- Transactions associated with age 34 have the highest number of fraud transactions, followed by 52,32, 43, and 61.

### Modelling

- The dataset was highly imbalanced, so stratified sampling was used for training and testing data split. Categorical features such as gender, state, and category are encoded using OneHotEncoder. All the numerical features are standardized using StandardScaler. Credit card fraud detection is a supervised classification problem. Multiple classification algorithms, such as decision trees, random forest, XGBClassifier, and logistic regression, were tested for this project. XGBClassifier model was selected to identify fraudulent credit card transactions over other models because of its better performance metrics.

A comparison of the performance metrics of the different models
<p align="left">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/comparison_of_the_performance_metrics.png" width="1400" height="300"/>
</p>

#### XGBClassifier

##### Confusion Matrix

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/confusion_matrix.png" width="750" height="500"/>
</p>

##### ROC Curve

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/roc_curve.png" width="750" height="500"/>
</p>

##### Feature Importance

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/creditcard-fraud-detection/images/importances_features.png" width="750" height="500"/>
</p>

- XGBClassifier model identified that features grocery POS, gas transport, transaction amount, transaction hour, travel, grocery net, female gender, age, state VA, and entertainment are the top 10 feature importances.
