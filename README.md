# Solar-Efficiency-Detection

## Predicting Solar Panel Efficiency Using Machine Learning


### Step-by-Step Methodology:

1. Data Preprocessing:
        ◦ Checked for direct NaN values.
        ◦ Identified and treated invalid placeholders such as 0 in temperature, 0 in wind_speed, etc., based on domain logic.
        ◦ Replaced invalid entries using median imputation to preserve central tendency without being affected by skewness.

2. Data Type Correction:
        ◦ Converted incorrect object types (e.g., humidity, wind_speed, pressure) to numeric values using pd.to_numeric() after proper cleaning.

3. Encoding Categorical Variables:
        ◦ Applied One-Hot Encoding on categorical variables like string_id, error_code, and installation_typeusing pd.get_dummies().

4. Feature Binning:
        ◦ Binned panel_age and maintenance_count into meaningful discrete intervals to reduce noise and improve learning.

5. Feature Scaling:
        ◦ Applied StandardScaler to all continuous numerical columns including newly engineered features to standardize distributions, allowing optimal model convergence.
        ◦ Negative values post-scaling are acceptable and expected due to standardization.

6. Feature Engineering:
        ◦ Created new features:
            ▪ power_output = voltage * current
            ▪ temperature_diff = temperature - module_temperature
            ▪ irradiance_per_cloud = irradiance / (cloud_coverage + 1)
            ▪ efficiency_drop_due_to_age = panel_age * soiling_ratio
            ▪ env_pressure_effect = pressure / (wind_speed + 1)

7. Handling Outliers:
        ◦ Utilized IQR method with multiplier factor 3 instead of 1.5 to reduce loss of valid extreme data points.
        ◦ Outlier count printed for each feature using a custom function.

8. Model Building and Evaluation:
        ◦ Tried multiple models (Random Forest, Polynomial Regression, Neural Networks).
        ◦ Final model with best score:
            ▪ LightGBM (Gradient Boosting Framework)
            ▪ Best result achieved with this model after preprocessing, feature engineering, and scaling.
        ◦ Score formula: Score = 100 * (1 - RMSE)
            ▪ Final Score: ~89.21

9. Model Output and Submission:
        ◦ Predicted the efficiency values for the test dataset.
        ◦ Combined predictions with the corresponding id values.
        ◦ Exported final submission as sample_submission.csv with two columns: id, efficiency.
   
## Conclusion
The pipeline built for this problem incorporated thorough data preprocessing, proper handling of invalid values, feature engineering, and robust model selection. The LightGBM model provided the highest accuracy with an RMSE-derived score of ~89.21, making it a strong candidate for deployment in real-world solar efficiency monitoring systems.
