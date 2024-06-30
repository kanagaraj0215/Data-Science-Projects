## Airbnb Pricing Assistant

**Airbnb:** <br />
Airbnb(Air Bed and Breakfast) is an American online marketing place for short-term and long-term homestays. It helps to connect homeowners with guests who are looking for accommodation. The company started in 2008, but it became popular in late 2014.

**Objective:** <br />
Airbnb often faces the business problem of setting a fair price. The listing price should be reasonable. The company must suggest a better price to guests so it doesn't lose customers to competitors such as Vrbo, Expedia, and TripAdvisor. This project aims to develop a machine-learning model to predict the price that Airbnb can suggest to guests based on various features such as location, number of bedrooms and bathrooms, property type, and customer ratings. 

**Data Source:** <br />
The dataset is sourced from the open-source website Kaggle. The dataset contains 23 columns such as id, name, host_id, host_name, neighbourhood_group, neighborhood, latitude, longitude, room_type, price, minimum_nights, number_of_reviews, last_review, reviews_per_month, calculated_host_listings_count, availability_365, review_scores_rating, review_scores_accuracy, review_scores_cleanliness, review_scores_checkin, review_scores_communication, review_scores_location and review_scores_value, and around 10000 observations.

**Data Preprocessing:** <br />

- All the values are null for the neighbourhood_group feature, which does not add value to the model. It is safe to drop the column. On the other hand, review features are missing more than 25% of the values, and we can't drop these fields because they positively correlate with the predictor variable price. Missing reviews are imputed with the mean value.
- Two possible outliers were in the dataset, and those were removed to reduce the bias in the model. 
- The fields host_id and id is system-generated, which is not helpful for the model. Also, the fields latitude and longitude are redundant, so they are dropped from the dataset.
- The price is skewed right; hence, a log transformation was applied to the price field, creating a new feature. 
- One hot encoding was applied to categorical fields, such as neighborhood and room type, and converted to numerical fields.

**Exploratory Data Analysis (EDA):** <br />

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/airbnb-pricing-assistant/images/Price_by_Room_Type.png" width="750" height="500"/>
</p>

- The above plot shows how the price is distributed across the room type. Most of the homes/apt are in the range of $10 to $2000, hotel rooms are in the range of $10 to $500, private rooms are in the range of $10 to $1500, and shared rooms are in the range of $10 to $500. We could see a $10000 price for the entire home/apt and private space. These numerical values would be an outlier.

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/airbnb-pricing-assistant/images/Histogram_of_the_price.png" width="750" height="500"/>
</p>

- The above histogram shows how the price is distributed. It clearly shows that it is not normally distributed and skewed right. It says that the mean is greater than the median. From the above boxplot, we already know that there are a few outliers, and these outliers might be contributing to the skewness.

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/airbnb-pricing-assistant/images/review_scores_vs_price.png" width="750" height="500"/>
</p>

- The above scatter plot shows that the price increases with high review scores, implying a positive correlation between the review score and the price.

<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/airbnb-pricing-assistant/images/heatmap.png" width="750" height="500"/>
</p>

- The above heat map shows the correlation between price and other numerical features. A positive correlation exists between the field price and the fields id, latitude, longitude, minimum_nights, calculated_host_listings_count, availability_365, review_scores_rating,review_scores_accuracy and review_scores_location. A negative correlation exists between the field price and the field host_id, number_of_reviews, reviews_per_month, review_scores_checkin, review_scores_communication, and review_scores_value.


### Modelling

- The Airbnb price prediction problem fits the regression model because the target variable is the continuous variable price. Metrics such as the R2 coefficient of determination, root mean square error, and absolute error are used as evaluation metrics.

A comparison of the performance metrics of the different models
<p align="center">
<img src="https://github.com/kanagaraj0215/Data-Science-Projects/blob/main/supervised-machine-learning/airbnb-pricing-assistant/images/comparison_of_the_performance_metrics.png" width="1400" height="300"/>
</p>


- OLS's coefficient of determination for the test dataset is 0.25, with a root mean square error of 0.7 and MAE of 0.54, which is much less than the average log price. We tried to tune the hyperparameter with the ridge regression, but the evaluation metrics look the same. Next, we tried using the KNN regression model, which yielded results almost similar to those of the OLS model. From the above three models, OLS seems to perform better.
