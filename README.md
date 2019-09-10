# User_Segmentation_Usage_Data

## Introduction
Based on survey results on users from 10 countries, combined with usage data from Duolingo for users included in the survey (Note: Usage data was collected from September 1, 2018 to November 5, 2018), the project tends to identify a set of user segments/personas and potential recommendations. With the cluster of similar users, it’ll provide direction for improving the product and marketing campaigns. 

## Methods
1. Explore the Data
  -	Analyze the Variable Distribution
  In high level, have an overview of columns’ data type, distribution of both categorical and numerical data. Create basic plot to support analysis.
  -	Assess the Missing Value
Check missing value percentage of all columns, decide whether remove or impute the missing values. In this case, due to limited number of data points and high missing value in important feature, choose to impute the missing values instead of removing directly.
  -	Impute the Missing Value
Use the most frequent value for categorical variables and mode for numerical variables.

2. Prepare the Data
  -	Format and Clean the Data
Considering fitting the categorical features into model, in this step do some necessary mapping shortening (some survey response category is too long). Also, map some columns into Boolean type.
  -	Transforming Skewed Variables
Check the skewness of all numeric columns and do log transform to reduce it. Algorithms can be sensitive to such distributions of values and can underperform if the range is not properly normalized.
  -	Normalizing Numerical Features
Applying a scaling to the data. It does not change the shape of each feature's distribution; however, normalization ensures that each feature is treated equally when applying supervised learners.

3. Preprocess the Data
  -	Encode the Categorical Variables – One-Hot-Encoding
Typically, learning algorithms expect input to be numeric, which requires that non-numeric features be converted. Here convert categorical variables by using the one-hot encoding scheme. Note: Since the test data is separate, in case there are unseen categories in test data which will fail the model, here use sklearn.OneHotEncoder rather the pd.get_dummies()
  -	Standardization
  -	Dimensionality Reduction – PCA
Apply principal component analysis on the data, thus finding the vectors of maximal variance in the data. Check out the ratio of variance explained by each principal component as well as the cumulative variance explained.
Plot the cumulative or sequential values. Based on that, select a value for the number of transformed features which will be retained for the clustering part of the project.

4. Initiate Clustering Instance – K-Means
  -	Choose appropriate k value – The Elbow Method
Apply k-means clustering to the dataset and use the average within-cluster distances from each point to their assigned cluster's centroid to decide on a number of clusters to keep.
  -	Fit the Model (on reduced dimensionality with chose k)
  -	Make the prediction
Use fitted model to get the predicted cluster labels which can be mapped back to the original data to dig deep on common characteristic of each clusters
Analyze the clustering result
  -	Plot the distribution graph of numerical and categorical features

## Findings & Recommendations
After analysis, choose k=4 in K-means model fitting, that is, cluster the users into 4 segments.  

__Segment Cluster 0 (Inactive user/ learner)__
=================================================================================
__Characteristic__  
Least average daily_goal, lowest courses_completed and courses_started, high days_on_platform, extremly small longest_streak, smaller active_days but with some proportion of big value, lower average highest_crown_count and course_progress	

__Description__  
This group of user seems very inactive or even give up learning at some moment in terms of smallest lessons_started/ completed, lowest longes_streak as well as days_on_platform.	

__Marketing/ Recommendation__  
No need to spend too much trying to retain


__Segment Cluster 1 (Active but slow learner)__  
=================================================================================
__Characteristic__  
Moderate average daily_goal (with more both lower and higher daily_goal), moderate courses_completed and courses_started, high days_on_platform, extremly small longest_streak, much higher average active_days, moderate average highest_crown_count and course_progress	

__Description__  
This group of user has enough day_on_platform, relatively moderate longest_streak, lessons completed/ started, but have very high active_days.	

__Marketing/ Recommendation__  
Probably they have enough motivation to learn but need to re-analyze the difficulty of the lessons which might increase the time for user to finish the lesson.  
Can design different lesson content or game for this group of users to encourage them.


__Segment Cluster 2 (Not committed user/ learner)__  
=================================================================================
__Characteristic__  
Moderate average daily_goal, very low courses_completed and courses_started, longer days_on_platform, extremly small longest_streak, very low and skewed average active_days, very low average highest_crown_count and course_progress	

__Description__  
This group of users is not very actively learning and using the app.	

__Marketing/ Recommendation__  
Aggressively encourage this group of users. Should send some more email or even longer reward free-trail of Duolingo Plus to increase the engagement.


__Segment Cluster 3 (Active user/ learner)__  
=================================================================================
__Characteristic__  
Higher average daily_goal, highest courses_completed and courses_started, longer days_on_platform, relatively low longest_streak, higher average active_days, higher average highest_crown_count and course_progress	

__Description__  
This group of users seem highly actively learners in terms of days_on_platform, active_days and courses started/ completed. However, the longest_streatk is relatively low.	

__Marketing/ Recommendation__  
Push some reminder or in-app rewards more appropriately to increase this group of user’s longest streak.
Focus no new products features (customized user experience), and loyalty programs

 
