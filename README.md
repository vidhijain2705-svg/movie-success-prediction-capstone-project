# Movie Success Prediction Analysis

##Project Overview

This capstone project focuses on building a Machine Learning classification model to classify movies into three categories:

- **Hit** — IMDb Score ≥ 6
- **Average** — IMDb Score ≥ 3 and < 6
- **Flop** — IMDb Score < 3

The project covers the complete Machine Learning workflow including data cleaning, exploratory data analysis, preprocessing, model building, evaluation and hyperparameter tuning.

## Project Objective

The objective of this project is to:

- Analyze the factors associated with movie success.
- Perform Exploratory Data Analysis (EDA) to identify patterns and relationships.
- Build classification models to classify movies as Hit, Average or Flop.
- Compare the performance of different Machine Learning algorithms.
- Understand the impact of class imbalance on model performance.

## Dataset

The original dataset contained:

- **5,043 rows**
- **28 columns**

After removing duplicate records:

- **4,998 movies** remained.

The dataset contains information such as:

- Budget
- Gross revenue
- Duration
- Genres
- Director and actor information
- Number of IMDb votes
- Critic and user reviews
- Facebook likes
- Language
- Country
- Content rating
- IMDb score
  

## Data Cleaning

The following data-cleaning steps were performed:

- Removed **45 duplicate records**.
- Handled missing numerical values using the **median**.
- Handled missing categorical values.
- Removed the `movie_imdb_link` column.
- Created the target variable `classify`.
- Excluded `imdb_score` from model features to prevent **target leakage**.
- Examined outliers and skewed numerical variables.


##  Exploratory Data Analysis

EDA was performed to understand distributions, relationships and patterns in the dataset.

Some important observations:

- IMDb scores were mainly concentrated between approximately **5 and 8**.
- Hit movies had a median duration of approximately **107 minutes**.
- Average movies had a median duration of approximately **97 minutes**.
- Flop movies had a median duration of approximately **92 minutes**.
- Median budget was approximately **20 million** across all three success categories.
- Strong correlations were identified between some numerical features.

A strong correlation of approximately **0.95** was observed between:

`actor_1_facebook_likes`

and

`cast_total_facebook_likes`

Therefore, `actor_1_facebook_likes` was removed to reduce multicollinearity.


##  Class Imbalance

The target variable was highly imbalanced:

| Movie Category | Number of Movies |
|---|---:|
| Hit | 3,556 |
| Average | 1,401 |
| Flop | 41 |

The very small number of Flop movies became an important limitation of the project.


## Data Preprocessing

The preprocessing stage included:

- Categorical encoding
- Feature selection
- Multicollinearity handling
- Separating independent variables (`X`) and target (`y`)
- 80/20 train-test split
- Stratified sampling
- Feature scaling using `StandardScaler` for Logistic Regression

The final model dataset contained **24 input features**.


## Machine Learning Models

The following classification algorithms were evaluated:
1. Logistic Regression
2. Decision Tree
3. Random Forest
Random Forest was also optimized using **GridSearchCV**.


# Model Performance

| Model | Accuracy | Hit Recall | Average Recall | Flop Recall | Macro F1 |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 75.6% | 92% | 36% | 0% | 0.44 |
| Decision Tree | 71.9% | 82% | 48% | 0% | 0.44 |
| Random Forest | **80.1%** | **94%** | 47% | 0% | 0.48 |
| Tuned Random Forest | 77.5% | 81% | **72%** | 0% | **0.50** |

Random Forest achieved the highest overall accuracy of **80.1%**.
However, because the dataset is highly imbalanced, accuracy alone was not considered sufficient for evaluating the models.


## Hyperparameter Tuning

Random Forest was tuned using **GridSearchCV with 3-fold cross-validation**.
The optimization metric used was **Macro F1**, so that each target class received equal importance.

Best parameters:

- `n_estimators = 100`
- `max_depth = 10`
- `min_samples_split = 5`
- `class_weight = balanced`

Best cross-validation Macro F1:
**0.546**

After tuning:
- Accuracy changed from **80.1% → 77.5%**
- Average Recall improved from **47% → 72%**
- Macro F1 improved from **0.48 → 0.50**

This demonstrates the trade-off between overall accuracy and balanced class performance.

---

## Key Findings

- Random Forest achieved the highest overall accuracy at **80.1%**.
- Hyperparameter tuning significantly improved prediction of the Average category.
- Average Recall increased from **47% to 72%**.
- Macro F1 improved from **0.48 to 0.50**.
- None of the models correctly identified the Flop category.
- Accuracy alone can be misleading when working with highly imbalanced datasets.


## Limitations

The major limitation is the severe class imbalance.
Only **41 movies** belonged to the Flop category.
After train-test splitting:
- Training Flops: **33**
- Testing Flops: **8**
This provided the models with very limited information for learning the characteristics of Flop movies.
Some variables such as gross revenue, number of votes and reviews are also generally available after a movie has been released. Therefore, the current project should be considered a historical classification model rather than a purely pre-release movie success forecasting system.


##  Future Scope

Future improvements could include:

- Collecting more balanced movie data, particularly more Flop examples.
- Exploring suitable class-balancing techniques.
- Improving categorical feature encoding.
- Further feature engineering.
- Creating better representations of genres, actors and directors.
- Building a true pre-release prediction model using only information available before movie release.
- Evaluating the model on newer or external movie datasets.

##  Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Scikit-learn


## Project Files

- `Data_Cleaning_and_EDA.ipynb` — Data cleaning and exploratory data analysis
- `feature_engineering and preprocessing.ipynb` — Feature engineering and preprocessing
- `Model Building and Evaluation.ipynb` — Model training, evaluation and hyperparameter tuning
- `movie_metadata.csv` — Original dataset
- `cleaned_movie_data.csv` — Cleaned dataset


## Author

**Vidhi Jain**

Machine Learning Capstone Project
