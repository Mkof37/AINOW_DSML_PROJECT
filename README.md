# AINOW_DSML_PROJECT

This project has been structured as a comprehensive data science pipeline, moving from raw data cleaning to advanced model evaluation. Here is the step-by-step implementation and the insights derived.

Step-by-Step Implementation
Library and Data Loading:

Essential libraries for data manipulation (pandas, numpy), visualization (seaborn, matplotlib), and machine learning (sklearn, xgboost) were imported.

The training dataset, consisting of 7,160 rows and 14 features, was loaded for analysis.

Exploratory Data Analysis (EDA):

Basic statistical summaries and data types were inspected. The dataset was found to have 7 categorical (object) columns and 7 numerical columns.

Missing values were identified in Garden (7), Building Dimension (106), Date_of_Occupancy (508), and Geo_Code (102).

Data Cleaning:

The NumberOfWindows column contained a '.' string representing missing data, which was replaced with NaN and converted to a numeric float.

Numerical Imputation: Missing values in Building Dimension, Date_of_Occupancy, and NumberOfWindows were filled using the median strategy.

Categorical Imputation: Missing values in Geo_Code and Garden were filled using the mode (most frequent value).

Feature Engineering:

A new feature, Building_Age, was calculated as: YearOfObservation - Date_of_Occupancy.

The Customer Id column was dropped as it provided no predictive value.

Data Transformation:

Categorical variables (Building_Painted, Building_Fenced, Garden, Settlement, Geo_Code) were transformed into numerical formats using Label Encoding to make them compatible with the models.

Model Training and Evaluation:

The data was split into training and validation sets.

Two models were implemented: Random Forest Classifier and XGBoost Classifier.

Performance was evaluated using accuracy, F1-score, and feature importance rankings.

Insights Derived
Dominant Predictors: The physical attributes of the building are the strongest indicators of a claim. Building Dimension is the single most important feature (31.8% importance), followed by the Geo_Code (20.1%).

Temporal Impact: The newly created Building_Age feature is a significant predictor (12.0% importance), suggesting that the age of the structure at the time of observation influences the likelihood of an insurance claim.

Model Performance: Both Random Forest and XGBoost achieved a solid baseline accuracy of 78%.

Class Imbalance Challenge: The models showed high precision for predicting non-claims (Class 0) but struggled with lower recall for actual claims (Class 1). This indicates that while the models are accurate overall, they find it difficult to correctly identify the minority of cases where a claim actually occurs.

Feature Sensitivity: Features like Settlement, Building_Fenced, and Garden had very low importance (all < 1%), suggesting they have minimal impact on the prediction compared to building size and location.
