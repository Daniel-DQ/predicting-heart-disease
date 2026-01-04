Predicting Heart Disease:

Preface:

In this practice we are going to try and build models to predict Heart Disease using the following dataset.
This data set dates from 1988 and consists of four databases: Cleveland, Hungary, Switzerland, and Long Beach V. It contains 76 attributes, including the predicted attribute, but all published experiments refer to using a subset of 14 of them. The "target" field refers to the presence of heart disease in the patient. It is integer valued 0 = no disease and 1 = disease.
Contents of the dataset:
1.	age
2.	sex
3.	chest pain type (4 values)
4.	resting blood pressure
5.	serum cholestoral in mg/dl
6.	fasting blood sugar > 120 mg/dl
7.	resting electrocardiographic results (values 0,1,2)
8.	maximum heart rate achieved
9.	exercise induced angina
10.	oldpeak = ST depression induced by exercise relative to rest
11.	the slope of the peak exercise ST segment
12.	number of major vessels (0-3) colored by flourosopy
13.	thal: 0 = normal; 1 = fixed defect; 2 = reversable defect
The names and social security numbers of the patients were recently removed from the database, replaced with dummy values.


Methodology:

First step is to review the dataset and clean the data. for this step we use EDA methods like finding and imputing missing and duplicate data , we check the datatypes of columns and check if a feature is skewed or unbalanced.
We used a heatmap plot to show the correlation matrix.
This is the summary of findings from first step:
highest correlations with Target are :cp, thalach, slope, exang, oldpeak, ca
'Age' has a relatively normal distribution.
fbs and sex are unbalanced.
fbs has the lowest correlation with target.
chol and oldpeak are right skewed.

Next step is preprocessing:

Splitting the data into train and test.
Because there are different types of features we used pipelines to help automate preprocessing .
Deviding features based on their types:
num_features = ['age', 'restbps', 'chol', 'thalach', 'oldpeak']
skewed_num_features = ['oldpeak', 'chol']
ordinal_features = ['fbs', 'restecg', 'slope', 'ca']
nominal_features = ['sex', 'cp', 'fbs', 'exang', 'thal']

Using pipelines, we have imputed and scaled required features and some more adjustments and in the end of this step the data is ready for model.
Next step is modeling:

we use 5 models(KNN, Logistic_Regression, LDA, QDA, Decision_Tree) and compare the results.
Used Precision, Recall, and F1-Scores to evaluate a models.
Results:
We can see the differences in models using ROC cure:
 

--- 10-Fold Cross-Validation (Robustness Check) ---
Model: KNN
  All 10 scores: [0.742 0.806 0.833 0.8   0.9   0.933 0.733 0.8   0.8   0.733]
  Mean Accuracy: 0.808
  Std Deviation: 0.064
--------------------
Model: LogisticRegression
  All 10 scores: [0.871 0.871 0.833 0.8   0.9   1.    0.833 0.8   0.733 0.8  ]
  Mean Accuracy: 0.844
  Std Deviation: 0.069
--------------------
Model: DecisionTree
  All 10 scores: [0.935 0.742 0.733 0.667 0.767 0.833 0.733 0.633 0.733 0.733]
  Mean Accuracy: 0.751
  Std Deviation: 0.080
--------------------
Model: LDA
  All 10 scores: [0.871 0.871 0.8   0.767 0.867 1.    0.833 0.8   0.733 0.8  ]
  Mean Accuracy: 0.834
  Std Deviation: 0.070
--------------------
Model: QDA
  All 10 scores: [0.806 0.839 0.733 0.733 0.767 0.933 0.8   0.7   0.733 0.8  ]
  Mean Accuracy: 0.785
  Std Deviation: 0.064


Conclusion:

With evaluating the results it appears that LogisticRegression performed the best and  LDA is very close to it at second place.
This indicates that the relation between the features and the target is most likely linear and Logistic Regression and LDA can capture that relation well and it’s the reason why QDA did not perform better .
KNN and Decision-Tree have lower scores probably because they don’t fit well for this dataset.


Optional:
 

--- 10-Fold Cross-Validation (Robustness Check) ---
Model: RandomForest
  All 10 scores: [0.839 0.839 0.8   0.767 0.8   0.967 0.733 0.767 0.8   0.733]
  Mean Accuracy: 0.804 (±0.065)
------------------------------
Model: SVM
  All 10 scores: [0.774 0.871 0.833 0.8   0.867 1.    0.7   0.833 0.733 0.767]
  Mean Accuracy: 0.818 (±0.080)
------------------------------
Model: GaussianNB
  All 10 scores: [0.677 0.871 0.767 0.767 0.8   1.    0.8   0.733 0.733 0.8  ]
  Mean Accuracy: 0.795 (±0.084)
------------------------------

Conclusion(Optional models):
These models have performed better according to ROC-Curve and AUC, but don’t have higher accuracy with 10-Fold Cross-Validation.

