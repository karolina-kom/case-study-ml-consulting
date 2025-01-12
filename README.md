# Predicting Student Performance Using Machine Learning

1. Introduction
In this project, I aimed to predict student performance based on various features, including demographic, academic, and school-related data. The task was to apply multiple machine learning models and evaluate their performance to make accurate predictions of student final grades.

2. Dataset Overview
The dataset I used in this project was the [Student Performance Data Set](https://archive.ics.uci.edu/ml/datasets/Student+Performance) from the UCI Machine Learning Repository.

The dataset includes features such as:
- Grades: first period (G1) and second period (G2) grades in Math and Portuguese subjects.
- Demographic: sex, age, address, family size, parents' occupations etc.
- Social: free time, alcohol comsumption, going out etc.
- School: school, study time failures, absences etc.
- The target variable is G3, the final grade.

3. Data Preprocessing
Before training the models, the data was preprocessed to ensure it was clean and ready for use.

This included:
- Merged Math and Portuguese subject datasets using an inner join: only kept students present in both datasets using the features listed in the student-merge.R file.
- Combined columns: created new average/combined columns for remaining columns which were not used to merge the datasets (e.g. absences, guardian, studytime etc.)
- Average G1, G2, G3 columns: created new grade columns using the mean from the Math and Portuguese grade columns.
- Encoding categorical variables: Categorical features were handled appropriately.

4. Model Training and Evaluation
4.1 Cross-Validation Results (Excluding G1 and G2)
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

![cross_validation_plot](../visualisations/cross_validation.png)

Based on these results, the Decision Tree model was excluded from the final evaluation due to its high variability and poor performance.

4.2 Final Model Evaluation (Including G1 and G2)
Excluding G1 and G2 features, the Random Forest Regressor and Linear Regression models were evaluated:

**Random Forest:**
- Mean Squared Error (MSE): 7.5308
- R² Score: 0.3472

**Linear Regression:**
- Mean Squared Error (MSE): 12.6722
- R² Score: -0.0984

Random Forest performed significantly better than Linear Regression, showing higher R² and lower MSE.

5. Model Interpretation and Feature Importance
The Random Forest model identified several key features as important in predicting student performance:

- Previous Grades (G1 and G2): These were the most influential factors in determining the final grade.
- Absences: High absenteeism was strongly associated with lower academic performance.
- Failures: The number of past failures also had a considerable impact on future performance.
- Health: Students’ self-reported health influenced performance, with poor health leading to lower grades.

6. Visualizations
Below are some visualizations that summarize key findings from the analysis:

Feature Importance (Random Forest)

Model Performance Comparison

7. Insights and Recommendations
Based on the results, I provide the following recommendations for educators:

- Monitor Absenteeism: Reducing absenteeism can help improve student performance.
- Support Students with Previous Failures: Target interventions for students who have failed in the past.
- Consider Health Factors: Ensure students with health issues are provided with accommodations.
- Encourage Early Academic Success: Support students early in their academic career, particularly those with low prior grades.

8. Conclusion
The Random Forest Regressor performed the best, with a high R² score and low MSE. It is an effective model for predicting student performance, providing valuable insights into the key factors that influence academic outcomes.


