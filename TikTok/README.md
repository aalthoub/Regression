# Overview 

At TikTok, their mission is to inspire creativity and bring joy. 

TikTok users have the ability to submit reports that identify videos and comments that contain user claims. These reports identify content that needs to be reviewed by moderators. The process generates a large number of user reports that are challenging to consider in a timely manner. 

This project is to develope a predictive model that can determine whether a video contains a claim or offers an opinion. With a successful prediction model, TikTok can reduce the backlog of user reports and prioritize them more efficiently.

# Project Background

This project is a claims classification project. The following tasks are needed at this stage of the project:

1. Determine the correct modeling approach
2. Build a regression model
3. Finish checking model assumptions
4. Evaluate the model
4. Interpret model results and summarize findings for cross-departmental stakeholders within TikTok

# Data Understanding
The data consisted of approximately 20k user submissions and 11 features. The features are listed below: 

| #  | Column                   | Non-Null Count | Dtype    |
|----|--------------------------|----------------|----------|
| 0  | claim_status             | 19084 non-null | object   |
| 1  | video_id                 | 19382 non-null | int64    |
| 2  | video_duration_sec       | 19382 non-null | int64    |
| 3  | video_transcription_text | 19084 non-null | object   |
| 4  | verified_status          | 19382 non-null | object   |
| 5  | author_ban_status        | 19382 non-null | object   |
| 6  | video_view_count         | 19084 non-null | float64  |
| 7  | video_like_count         | 19084 non-null | float64  |
| 8  | video_share_count        | 19084 non-null | float64  |
| 9  | video_download_count     | 19084 non-null | float64  |
| 10 | video_comment_count      | 19084 non-null | float64  |


Another feature was engineered to represent different information as shown below:
- `video_transcription_text_length` to capture the length for each transcription text

Below is a visualization of the distribution of `video_transcription_text` length for videos posted by: 
1. Verified accounts 
2. Unverified accounts

![Visualize the distribution of `video_transcription_text`](/Regression/images/1.png)

# Modeling and Evaluation 
The confusion matrix below visualizes the results of the logistics regression model.
![Plot to show the Homoscedasticity](Regression/images/2.png)

**Insights:**
- The upper-left quadrant displays the number of videos posted by unverified accounts that the model accurately classified as so.

- The upper-right quadrant displays the number of videos posted by unverified accounts that the model misclassified as posted by verified accounts.

- The lower-left quadrant displays the number of videos posted by verified accounts that the model misclassified as posted by unverified accounts.

- The lower-right quadrant displays the number of videos posted by verified accounts that the model accurately classified as so.

**Note**: A perfect model would yield all true negatives and true positives (upper left and lower right quadrants), and no false negatives or false positives.


# Conclusion

1. The dataset has a few strongly correlated variables, which might lead to multicollinearity issues when fitting a logistic regression model. We decided to drop `video_like_count` from the model building.

2. Based on the logistic regression model, each additional second of the video is associated with 0.01 increase in the log-odds of the user having a verified status.

3. The logistic regression model had decent predictive power: a precision of 69% and a recall of 66% (weighted averages), and it achieved an accuracy of 66%.

