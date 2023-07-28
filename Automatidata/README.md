# Overview 
The goal of this project was to create a multiple linear regression to predict taxi fares. This project utilized yellow taxi trips taken in New York City during 2017. The final model performance is high on both training and test sets, with 89% R2, 1.99 MAE, 12.1 MSE and 3.48 RMSE determining what features were most important. Based on the model, the mean_duration and mean_distance were the most influential in determining taxi fares. 

# Data Understanding
The NYC Taxi and Limousine Commission data came from NYC.gov. The data consisted of approximately 408k unique trips and 18 features. The features included information on trip duration and destination, vendor used, toll information, and payment type. 

Other features were engineered to represent different information as shown below:
- `mean_distance` to capture the mean distance for each group of trips that share pickup and dropoff points.
- `mean_duration` to capture the mean duration for each group of trips that share pickup and dropoff points.
- `rush_hour` to capture if a ride was taken during rush hour or not

Multiple redundant columns were dropped and reformatted into the proper data type.

# Modeling and Evaluation 
The below plots show that the performance of the prediction model by evaluating the three main assumptions of the results – Homoscedasticity, Normality and Linearity – respectively. 

![Plot to show the Homoscedasticity](/Automatidata/images/1.png)
 
![Plot to show the Homoscedasticity](/Automatidata//images/2.png)
- **Insight**: The distribution of the residuals is normal and has a mean of -0.015. This normal distribution around zero is good, as it demonstrates that the model errors are evenly distributed and unbiased.

![Plot to show the Homoscedasticity](/Automatidata//images/3.png)
- **Insight**: The model's residuals are evenly distributed above and below zero, with the exception of the sloping lines from the upper-left corner to the lower-right corner, which they represent the imputed maximum of \$62.50 and the flat rate of \$52 for JFK airport trips.


# Conclusion
The coefficients reveal that `mean_distance` was the feature with the greatest weight in the model's final prediction. For every mile traveled, the fare amount increases by a mean of $7. However, because some highly correlated features were not removed, the confidence interval of this assessment is wider.

