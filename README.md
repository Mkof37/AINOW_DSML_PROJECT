# AINOW_DSML_PROJECT

This project has been structured as a comprehensive data science pipeline, moving from raw data cleaning to advanced model evaluation. Here is the step-by-step implementation and the insights derived.

**Step-by-Step Implementation**

**1. Library and Data Loading:**

* Essential libraries for data manipulation (pandas, numpy), visualization (seaborn, matplotlib), and machine learning (sklearn, xgboost) were imported.

* The training dataset, consisting of 7,160 rows and 14 features, was loaded for analysis.

**2. Data Cleaning and Preprocessing :**

* Basic statistical summaries and data types were inspected. The dataset was found to have 7 categorical (object) columns and 7 numerical columns.

* Missing values were identified in Garden (7), Building Dimension (106), Date_of_Occupancy (508), and Geo_Code (102).
* The NumberOfWindows column contained a '.' string representing missing data, which was replaced with NaN and converted to a numeric float.

* Numerical Imputation: Missing values in Building Dimension, Date_of_Occupancy, and NumberOfWindows were filled using the median strategy.

* Categorical Imputation: Missing values in Geo_Code and Garden were filled using the mode (most frequent value).
  
* Categorical variables (Building_Painted, Building_Fenced, Garden, Settlement, Geo_Code) were transformed into numerical formats using Label Encoding to make them compatible with the models.
  
**3. Exploratory Data Analysis (EDA) Insights:**

From the visualizations, several critical insights were extracted:

*	Class Imbalance: The target variable Claim is imbalanced, with claims accounting for approximately 22% of the records. This requires using metrics like AUC-ROC and F1-score rather than simple accuracy.

*	Dimension Impact: The "Building Dimension vs Claim" boxplot revealed that buildings with claims typically have a larger physical footprint (higher median $m^2$) compared to those without claims.

*	Building Type Risks: Certain Building_Type categories show a higher ratio of claims, suggesting structural designs or materials in specific types are more prone to insured risks.

*Urban vs Rural: Settlement patterns (U vs R) impact claim frequency, with urban areas generally showing more activity, possibly due to higher density or reporting rates.



**4. Feature Engineering:**

* A new feature, Building_Age, was derived by calculating the difference between the YearOfObservation and the Date_of_Occupancy. This captures the lifecycle risk of the building.

* The Customer Id column was dropped as it provided no predictive value.

**5. Model Training and Evaluation:**

* The dataset was split into an 80% training set and a 20% validation set, ensuring the class distribution was maintained (stratified split).

* Two models were implemented: Random Forest Classifier and XGBoost Classifier.

* Performance was evaluated using accuracy, F1-score, and feature importance rankings.

**Insights Derived**
* **Dominant Predictors:** The physical attributes of the building are the strongest indicators of a claim. Building Dimension is the single most important feature (31.8% importance), followed by the Geo_Code (20.1%).

* **Temporal Impact:** The newly created Building_Age feature is a significant predictor (12.0% importance), suggesting that the age of the structure at the time of observation influences the likelihood of an insurance claim.

* **Model Performance:** Both Random Forest and XGBoost achieved a solid baseline accuracy of 78%.

* **Class Imbalance Challenge**: The models showed high precision for predicting non-claims (Class 0) but struggled with lower recall for actual claims (Class 1). This indicates that while the models are accurate overall, they find it difficult to correctly identify the minority of cases where a claim actually occurs.

* **Feature Sensitivity:** Features like Settlement, Building_Fenced, and Garden had very low importance (all < 1%), suggesting they have minimal impact on the prediction compared to building size and location.

**Model Comparison**
*	Gradient Boosting achieved the highest AUC-ROC (0.696), making it the best model for ranking buildings by their probability of having a claim.

*	Random Forest showed that Building Dimension and Geo_Code are the most influential variables in predicting a claim event.

**Final Recommendation**
The Gradient Boosting model is recommended for its superior ability to distinguish between claim and no-claim risks (AUC). However, the insurance company should use the probability outputs rather than hard classifications to set different premium tiers based on the risk scores.

