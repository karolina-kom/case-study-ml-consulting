# Predicting Student Performance Using Machine Learning

## Introduction
This project aims to identify the most important demographic, social, academic, and school-related features that influence student performance. The task was to apply machine learning models and evaluate their performance to make accurate predictions of student final grades.

## Dataset Overview
The dataset used in this project is the [Student Performance Data Set](https://archive.ics.uci.edu/ml/datasets/Student+Performance) from the UCI Machine Learning Repository.

The dataset includes features such as:
- Grades: first period (G1), and second period (G2) grades in Math and Portuguese subjects.
- Demographic: sex, age, address, family size, parents' occupations etc.
- Social: free time, alcohol comsumption, going out etc.
- School: school, study time failures, absences etc.

The target variable is G3, the final grade in Math and Portuguese.

## Data Preprocessing
Before training the models, the data was preprocessed to ensure it was clean and ready for use.

This included:
- **Merging the Math and Portuguese subject datasets**: only kept students present in both datasets by performing an inner merge using the features listed in the student-merge.R file.
- **Combining remaining feature columns**: created new average/combined columns for remaining feature columns which were not used to merge the datasets (e.g. absences, guardian, studytime etc.)
- **Creating average G1, G2, G3 columns**: created new grade columns using the mean from the Math and Portuguese grade columns.
- **Encoding categorical variables**: Categorical features were handled appropriately.

## Data Exploration
### Distribution of G3 grades

![G3_subject_grade_distribution_plot](/visualisations/G3_mat_por_distribution.png)
![G3_average_grade_distribution_plot](/visualisations/G3_avg_distribution.png)

### Correlation Matrix

![correlation_matrix_plot](/visualisations/correlation_matrix.png)

### Key Feature Relationship

![G3_average_absence_scatter_plot](/visualisations/G3_avg_absence_scatter.png)

## Model Training and Evaluation
### Feature Selection
The G1 and G2 grades are highly correlated with the final G3 grade. After exploring the relationship between G1 and G3, and G2 and G3, I decided to train and evaluation the model by exlucding and including G1 and G2.

![G1_avg_G3_avg_scatter](/visualisations/G1_avg_G3_avg_scatter.png)
![G2_avg_G3_avg_scatter](/visualisations/G2_avg_G3_avg_scatter.png)

### Cross-Validation Results
To evaluate the models’ performance, I applied cross-validation. Below are the results for the models evaluated:

**Decision Tree:**
- Mean MSE: -17.92
- Standard Deviation: 4.55
  
**Random Forest:**
- Mean MSE: -9.33
- Standard Deviation: 2.63
  
**Linear Regression:**
- Mean MSE: -10.04
- Standard Deviation: 3.66

![cross_validation_plot](/visualisations/cross_validation.png)

Based on these results, the Decision Tree model was excluded from the final evaluation due to its high variability and poor performance.

### Final Model Evaluation
Excluding G1 and G2 features, the Random Forest Regressor and Linear Regression models were evaluated:

**Random Forest:**
- Mean Squared Error (MSE): 7.5308
- R² Score: 0.3472

**Linear Regression:**
- Mean Squared Error (MSE): 12.6722
- R² Score: -0.0984

Random Forest performed significantly better than Linear Regression, showing higher R² and lower MSE.

## Model Interpretation and Feature Importance
The Random Forest model identified several key features as important in predicting student performance:

- Previous Grades (G1 and G2): These were the most influential factors in determining the final grade.
- Absences: High absenteeism was strongly associated with lower academic performance.
- Failures: The number of past failures also had a considerable impact on future performance.
- Health: Students’ self-reported health influenced performance, with poor health leading to lower grades.

![feature_importance_g1_g2](/visualisations/feature_importance_g1_g2.png)
![feature_importance_no_g1_g2](/visualisations/feature_importance_no_g1_g2.png)

## Insights and Recommendations
Based on the results, I provide the following recommendations for educators:

- **Monitor Absenteeism**: Reducing absenteeism can help improve student performance.
- Support Students with Previous Failures: Target interventions for students who have failed in the past.
- **Consider Health Factors**: Ensure students with health issues are provided with accommodations.
- **Encourage Early Academic Success**: Support students early in their academic career, particularly those with low prior grades.

## Conclusion
The Random Forest Regressor performed the best, with a high R² score and low MSE. It is an effective model for predicting student performance, providing valuable insights into the key factors that influence academic outcomes.
