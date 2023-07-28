# Overview 

Waze’s free navigation app makes it easier for drivers around the world to get to where they want to go. Waze’s community of map editors, beta testers, translators, partners, and users helps make each drive better and safer. Waze partners with cities, transportation authorities, broadcasters, businesses, and first responders to help as many people as possible travel more efficiently and safely. 

This project is part of a larger effort at Waze to increase growth. Typically, high retention rates indicate satisfied users who repeatedly use the Waze app over time. Developing a churn prediction model will help prevent churn, improve user retention, and grow Waze’s business. An accurate model can also help identify specific factors that contribute to churn and answer questions such as: 

- Who are the users most likely to churn?
- Why do users churn? 
- When do users churn? 

For example, if Waze can identify a segment of users who are at high risk of churning, Waze can proactively engage these users with special offers to try and retain them. Otherwise, Waze may lose these users without knowing why. 

# Project Background

The following tasks are needed at this stage of the project:

1. Determine the correct modeling approach
2. Build a regression model
3. Finish checking model assumptions
4. Evaluate the model


# Data Understanding
The data consisted of approximately 15k rows and 11 columns. The features are listed below: 

| #   | Column                  | Non-Null Count | Dtype     |
|-----|-------------------------|----------------|-----------|
| 0   | ID                      | 14999 non-null | int64     |
| 1   | label                   | 14299 non-null | object    |
| 2   | sessions                | 14999 non-null | int64     |
| 3   | drives                  | 14999 non-null | int64     |
| 4   | total_sessions          | 14999 non-null | float64   |
| 5   | n_days_after_onboarding | 14999 non-null | int64     |
| 6   | total_navigations_fav1  | 14999 non-null | int64     |
| 7   | total_navigations_fav2  | 14999 non-null | int64     |
| 8   | driven_km_drives        | 14999 non-null | float64   |
| 9   | duration_minutes_drives | 14999 non-null | float64   |
| 10  | activity_days           | 14999 non-null | int64     |
| 11  | driving_days            | 14999 non-null | int64     |
| 12  | device                  | 14999 non-null | object    |


Some features were engineered to represent different information as shown below:
- `km_per_driving_day`, which represents the mean distance driven per driving day for each user
- `professional_driver` that is a 1 for users who had 100 or more drives and drove on 15+ days in the last month, and 0 otherwise

Other features either dropped or encoded upon building the model.

Below is a visualization of the correlation among the predictor variables: 
![Visualize the correlation](/Waze/images/1.png)

**Insight**
The following predictors are strongly multicollinear as they have a Pearson correlation coefficient value greater than the **absolute value of 0.7**:
- `sessions` and `drives` have a correlation coefficient value of 1.0
- `driving_days` and `activity_days`: have a correlation coefficient value of 0.95

**Note:** 0.7 is an arbitrary threshold. Some industries may use 0.6, 0.8, etc.

Below is a visualization of the linear relationship between predictor variables and the estimated log odds (known as logits):
![Linear relationship between predictor variables and the estimated log odds](/Waze/images/2.png)

**Rule:**
In **logistic regression**, the relationship between a predictor variable and the dependent variable does not need to be linear, however, the log-odds (a.k.a logit) of the dependent variable with respect to the predictor variable should be linear. Here is the formula for calculating log-odds, where _p_ is the probability of response:
                            </br>
                            $$ 
                            logit(p) = ln(\frac{p}{1-p}) 
                            $$
                            <br/>

# Modeling and Evaluation 
The confusion matrix below visualizes the results of the logistics regression model:
![Confusion Matrix](/Waze/images/3.png)

The barplot below visualizes the model's coefficients to show the importance of the model's features:
![Barplot](/Waze/images/4.png)


# Conclusion

> _`activity_days` was by far the most important feature in the model. It has a negative correlation with user churn. This was not surprising, as this variable was very strongly correlated with `driving_days`, which was known from EDA to have a negative correlation with churn._

> The correlation heatmap revealed the `km_per_driving_day` variable to have the strongest positive correlation with churn of any of the predictor variables by a relatively large margin. It was the second-least-important variable.

> _New features could be engineered to try to generate better predictive signal, as they often do if you have domain knowledge. In the case of this model, one of the engineered features (`professional_driver`) was the third-most-predictive predictor. It could also be helpful to scale the predictor variables, and/or to reconstruct the model with different combinations of predictor variables to reduce noise from unpredictive features._

> _It would be helpful to have drive-level information for each user (such as drive times, geographic locations, etc.). It would probably also be helpful to have more granular data to know how users interact with the app. For example, how often do they report or confirm road hazard alerts? Finally, it could be helpful to know the monthly count of unique starting and ending locations each driver inputs._
