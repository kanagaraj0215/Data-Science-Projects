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
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/CreditCard-Fraud-Detection/Histogram_of_Amount.png" width="750" height="500"/>
</p>

- The higher amount misinterprets the histogram. Hence, the 0.99 quantile was used to remove the noise. The histogram shows that the data is skewed right.
