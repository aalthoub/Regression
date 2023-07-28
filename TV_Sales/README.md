# Project Background 

This project is to analyze a small business' historical marketing promotion data. Each row corresponds to an independent marketing promotion where the business uses TV, social media, radio, and influencer promotions to increase sales.

The following tasks are needed at this stage of the project:

1. Determine the correct modeling approach
2. Build a regression model
3. Finish checking model assumptions
4. Evaluate the model


# Data Understanding
The data consist of approximately 570 rows and 5 columns. The features are listed below: 

| Column       | Non-Null Count | Dtype    |
| ------------ | -------------- | -------- |
| TV           | 572            | object   |
| Radio        | 572            | float64  |
| Social Media | 572            | float64  |
| Influencer   | 572            | object   |
| Sales        | 572            | float64  |


Below is a pairplot to visualize the relationship between the continous variables
![pairplot](/TV_Sales/images/1.png)

**Insight** 
`Radio` and `Social Media` both appear to have linear relationships with `Sales`. Notice that `TV` and `Influencer` are excluded from the pairplot because they are not numeric. 

# Modeling and Evaluation 
The following is the results of the OLS regression model:
![OLS Results](/TV_Sales/images/2.png)

**Interpret Model Coefficients** 
- Using `TV` and `Radio` as the independent variables results in a multiple linear regression model with $R^{2} = 0.904$. In other words, the model explains $90.4\%$ of the variation in `Sales`. This makes the model an excellent predictor of `Sales`. 

- The default `TV` category for the model is `High` since there are coefficients for the other two `TV` categories, `Medium` and `Low`. Because the coefficients for the `Medium` and `Low` `TV` categories are negative, that means the average of sales is lower for `Medium` or `Low` `TV` categories compared to the `High` `TV` category when `Radio` is at the same level. For example, the model predicts that a `Low` `TV` promotion is 154.2971 lower on average compared to a `high` `TV` promotion given the same `Radio` promotion.

- The coefficient for `Radio` is positive, confirming the positive linear relationship shown earlier during the exploratory data analysis.

- The p-value for all coefficients is $0.000$, meaning all coefficients are statistically significant at $p=0.05$. The 95% confidence intervals for each coefficient should be reported when presenting results to stakeholders. For example, there is a $95\%$ chance that the interval $[-163.979,-144.616]$ contains the true parameter of the slope of $\beta_{TVLow}$, which is the estimated difference in promotion sales when a `Low` `TV` promotion is chosen instead of a `High` `TV` promotion.

## Model Assumtion: Linearity
![Linearity](/TV_Sales/images/3.png)

**Insight**
The linearity assumption holds for `Radio`, as there is a clear linear relationship in the scatterplot between `Radio` and `Sales`. Also, the `Social_Media` does appear to have a linear relationship with `Sales`.

## Model Assumtion: Normality
![Linearity](/TV_Sales/images/4.png)

**Insight** 
- The histogram of the residuals are approximately normally distributed, which supports that the normality assumption is met for this model. 
- The residuals in the Q-Q plot form a straight line, further supporting that this assumption is met.

## Model Asuumption: Contant Variance
![Linearity](/TV_Sales/images/5.png)

**Insight**
The fitted values are in three groups because the categorical variable is dominating in this model, meaning that TV is the biggest factor that decides the sales. However, the variance where there are fitted values is similarly distributed, validating that the assumption is met.

## Model Asuumption: Multicollinearity
The model only has one continous independent variable, meaning there are no multicollinearity issues. 

# Conclusion

> _High TV promotional budgets have a substantial positive influence on sales. The model estimates that switching from a high to medium TV promotional budget reduces sales by $\$75.3120$ million (95% CI $[-82.431,-68.193])$, and switching from a high to low TV promotional budget reduces sales by $\$154.297$ million (95% CI $[-163.979,-144.616])$._ 

> _The model also estimates that an increase of $\$1$ million in the radio promotional budget will yield a $\$2.9669$ million increase in sales (95% CI $[2.551,3.383]$). Thus, it is recommended that the business allot a high promotional budget to TV when possible and invest in radio promotions to increase sales._ 
