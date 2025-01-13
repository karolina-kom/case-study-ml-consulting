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
- **Handling missing data**: checked for missing data after merging datasets.
- **Combining remaining feature columns**: created new average/combined columns for remaining feature columns which were not used to merge the datasets (e.g. absences, guardian, studytime etc.)
- **Creating average G1, G2, G3 columns**: created new grade columns using the mean from the Math and Portuguese grade columns.
- **Encoding categorical variables**: Categorical features were handled appropriately.

## Data Exploration
I performed a few data exploration steps to investigate the data further. 

### Distribution of G3 grades
Below are two plots: one of the distribution of the final G3 grade for individual subjects (Mathematics and Portuguese), and one of the distribution of the final G3 grade taking the mean of both subjects for each students. 

![G3_subject_grade_distribution_plot](/visualisations/G3_mat_por_distribution.png)
![G3_average_grade_distribution_plot](/visualisations/G3_avg_distribution.png)

Based on the distributions, I decided to look at the average G3 grade instead of the G3 values for individual subjects. The distribution of grades is much smoother and closer to a normal distribution, and using the average G3 grade will give more an insight into overall academic performance, rather than subject-specific performance.

### Correlation Matrix
Next, I investigated the correlation between numeric features using a correlaton matrix. Features with high correlations will either be not be used to train the machine learning model or handled carefully.

![correlation_matrix_plot](/visualisations/correlation_matrix.png)

Based on the correlation matrix, we can see that G1 and G2 grades are highly correlated with the final G3 grade. Our aim is to investigate the features which influence student performance, so while past exam performance is important, we want to also consider features which educators have more influence over. Therefore, we will train the models twice: once including G1 and G2 as features, and once excluding G1 and G2 as features.

### Key Feature Relationship
I investigated the relationship between a key feature (absences) and the final G3 grade using a scatter plot.

![G3_average_absence_scatter_plot](/visualisations/G3_avg_absence_scatter.png)

Based on the scatter plot, we can see there is a weak relationship between absences and the final G3 grade (more absences results in a lower average grade.)

## Model Training and Evaluation
### Feature Selection
The G1 and G2 grades are highly correlated with the final G3 grade. After exploring the relationship between G1 and G3, and G2 and G3, I decided to train and evaluation the model using two feature sets: one including G1 and G2 and one excluding G1 and G2.

![G1_avg_G3_avg_scatter](/visualisations/G1_avg_G3_avg_scatter.png)
![G2_avg_G3_avg_scatter](/visualisations/G2_avg_G3_avg_scatter.png)

### Cross-Validation Results
To evaluate the models’ performance, I applied cross-validation. Below are the results for the model cross-validation:

| Model | Mean Squared Error (MSE) | Standard Deviation |
| ----------- | ----------- | ----------- |
| Decision Tree | -17.92 | 4.55 |
| Random Forest | -9.33 | 2.63 |
| Linear Regression | -10.04 | 3.66 |

The results are summarised in the plot below:

![cross_validation_plot](/visualisations/cross_validation.png)

Based on these results, the Decision Tree model was excluded from the final evaluation due to its high variability and poor performance. Given more time, I would have looked into pruning the decision tree and using fewer features to prevent overfitting, in order to improve the performance of the Decision Tree model.

### Final Model Evaluation
Below are the final model evaluation results for the Random Forest and Linear Regression models, using Mean Square Error (MSE) and R² Score metrics.

| Model | With/Without G1 and G2 | Mean Squared Error (MSE) | R² Score |
| ----------- | ----------- | ----------- | ----------- |
| Random Forest | With | 1.3672 | 0.8815 |
| Linear Regression | With | 2.2615 | 0.8040 |
| Random Forest | Without | 7.5308 | 0.3472 |
| Linear Regression | Without| 12.6722 | -0.0984 |

The results are summarised in the plot below:

![final results_plot](/visualisations/final_results.png)

We can see that both models perform significantly better when G1 and G2 are included as features. However, Random Forest performed better than Linear Regression using both feature sets, as it shows higher R² and lower MSE.

## Model Interpretation and Feature Importance
The Random Forest model identified several key features as important in predicting student performance:

- **Previous Grades (G1 and G2)**: These were the most influential factors in determining the final grade.
- **Absences**: High absenteeism was strongly associated with lower academic performance.
- **Failures**: The number of past failures also had a considerable impact on future performance.
- **Health**: Students’ self-reported health influenced performance, with poor health leading to lower grades.

The feature importances are summarised in the plots below:

![feature_importance_g1_g2](/visualisations/feature_importance_g1_g2.png)
![feature_importance_no_g1_g2](/visualisations/feature_importance_no_g1_g2.png)

## Insights and Recommendations
Based on the results, I provide the following recommendations for educators:

- **Monitor Absenteeism**: Reducing absenteeism can help improve student performance.
- **Support Students with Previous Failures**: Target interventions for students who have failed in the past.
- **Consider Health Factors**: Ensure students with health issues are provided with accommodations.
- **Encourage Early Academic Success**: Support students early in their academic career, particularly those with low prior grades.

## Conclusion
The Random Forest Regressor performed the best, with a high R² score and low MSE. It is an effective model for predicting student performance, providing valuable insights into the key factors that influence academic outcomes.
