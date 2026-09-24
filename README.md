# Movie Success Prediction Analysis
# Project Overview

This capstone project focuses on building a Machine Learning classification model to classify movies into three IMDb-rating-based success categories:

Hit — IMDb Score ≥ 6
Average — IMDb Score ≥ 3 and < 6
Flop — IMDb Score < 3

The project covers the complete Machine Learning workflow, including data cleaning, exploratory data analysis, preprocessing, feature selection, model building, model evaluation, comparison, and hyperparameter tuning.

# Project Objective

The objective of this project is to analyze different movie characteristics and build classification models that can categorize movies as Hit, Average, or Flop based on IMDb score ranges.

The project also aims to identify relationships between movie-related features and the IMDb-rating-based success categories and compare the performance of different Machine Learning classification algorithms.

# Dataset

The dataset contains information about movies, including:

Budget
Gross Revenue
Duration
Genres
Content Rating
Country and Language
Number of Voted Users
User Reviews
Critic Reviews
Movie Facebook Likes
Cast-related Facebook Likes
IMDb Score

After data cleaning, the final dataset contained 4,998 movie records.

# Target Variable

A new target variable called classify was created from imdb_score.

The categories are:

Flop: IMDb Score < 3
Average: IMDb Score ≥ 3 and < 6
Hit: IMDb Score ≥ 6

The final target distribution was:

Hit: 3,556 movies
Average: 1,401 movies
Flop: 41 movies

This shows that the target variable is highly imbalanced, particularly for the Flop category.

# Exploratory Data Analysis

EDA was performed to understand feature distributions, identify outliers, examine relationships between movie characteristics and the target variable, and detect correlations between numerical features.

# Important EDA Findings

Movie duration showed some variation across the success categories. The median duration was approximately 107 minutes for Hit movies, 97 minutes for Average movies, and 92 minutes for Flop movies.

For budget analysis, original reported values were used rather than median-imputed values. Median budgets were approximately:

Hit: $19.8 million
Average: $20.0 million
Flop: $19.0 million

The similarity between these values suggests that budget alone does not clearly distinguish the IMDb-rating-based success categories.

Gross revenue showed a clearer difference between categories. Using original reported gross values, median gross revenue was approximately:

Hit: $27.30 million
Average: $22.13 million
Flop: $9.11 million

This indicates an association between higher IMDb-rating-based success categories and higher gross revenue in this dataset.

# Correlation and Multicollinearity

A correlation heatmap was used to examine relationships between numerical features.

A strong positive correlation of approximately 0.95 was identified between actor_1_facebook_likes and cast_total_facebook_likes.

To reduce multicollinearity, actor_1_facebook_likes was removed from the model input.

# Feature Selection and Preprocessing

imdb_score was excluded from the input features because it was directly used to create the target variable. Including it would result in target leakage.

movie_title was excluded because it primarily acts as an identifier.

High-cardinality categorical variables were also excluded from the final model input:

director_name
actor_1_name
actor_2_name
actor_3_name
plot_keywords

These columns contained a large number of unique values, and directly applying Label Encoding would assign arbitrary numerical values to names and keywords.

The remaining categorical variables were converted into numerical form using Label Encoding.

After feature selection, 19 input features were used for model building.

The dataset was split into:

80% Training Data
20% Testing Data

Stratified sampling was used to preserve the target class distribution.

StandardScaler was applied where required to bring features onto a comparable scale.

# Machine Learning Models

# The following classification algorithms were evaluated:

* Logistic Regression
* Decision Tree Classifier
* Random Forest Classifier
* Tuned Random Forest Classifier
* Model Performance
* Model	Accuracy	Macro F1
* Logistic Regression	76.1%	0.44
* Decision Tree	73.0%	0.48
* Random Forest	80.3%	0.49
* Tuned Random Forest	77.9%	0.53

Random Forest achieved the highest overall accuracy at 80.3%.

However, because the dataset is highly imbalanced, accuracy alone was not considered sufficient for evaluating model performance.

Precision, recall, F1-score, Macro F1-score, and confusion matrices were also examined.

# Hyperparameter Tuning

Random Forest was further optimized using GridSearchCV.

Macro F1-score was used as the scoring metric to place greater emphasis on balanced performance across the three target classes.

The selected parameters were:

* class_weight: balanced
* max_depth: 10
* min_samples_split: 5
* n_estimators: 200

After tuning:

Accuracy changed from 80.3% to 77.9%.
Macro F1-score improved from 0.49 to 0.53.
Correct Average predictions increased from 135 out of 280 to 210 out of 280.
The tuned model correctly identified 1 out of 8 Flop movies, compared with zero correctly identified by the original Random Forest.

Therefore, tuning resulted in a trade-off between overall accuracy and more balanced class-level performance.

# Key Findings
* Random Forest achieved the highest overall accuracy of 80.3%.
* Tuned Random Forest achieved the highest Macro F1-score of 0.53.
* Budget alone did not clearly distinguish Hit, Average, and Flop categories.
* Gross revenue showed a clearer association with the IMDb-rating-based success categories.
* Severe class imbalance significantly affected prediction of the Flop category.
* Hyperparameter tuning improved the prediction of Average movies and slightly improved Flop detection.
* Accuracy alone can be misleading when evaluating an imbalanced classification problem.

# Project Limitations

* The dataset is highly imbalanced, with only 41 Flop movies.
* Flop prediction remained weak because of the limited number of Flop observations.
* Some numerical variables contain extreme or skewed values.
* Some features, such as gross revenue, user votes, and reviews, may contain post-release information. Therefore, the current model should not be considered a * purely pre-release forecasting system.
* Future improvements could focus on obtaining more balanced data and using more pre-release features.

# Conclusion

* This project demonstrates an end-to-end Machine Learning classification workflow for categorizing movies into Hit, Average, and Flop categories based on IMDb score ranges.
* The analysis showed that budget alone did not clearly differentiate the three success categories, while gross revenue showed a clearer association with IMDb-rating-based movie success.
* Random Forest achieved the highest overall accuracy of 80.3%. After hyperparameter tuning, accuracy decreased slightly to 77.9%, while Macro F1-score improved from 0.49 to 0.53, indicating more balanced performance across the target categories.
* The project highlights the importance of evaluating imbalanced classification models using precision, recall, F1-score, and Macro F1-score in addition to overall accuracy.

# Tools and Technologies
Python
Pandas
NumPy
Matplotlib
Seaborn
Scikit-learn
Jupyter Notebook

# BY VIDHI JAIN
