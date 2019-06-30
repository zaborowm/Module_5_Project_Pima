# Module_5_Project_Pima
Module 5 Individual Project - Predict a diagnosis of Diabetes from Pima Indian data set
Using a data set from the National Institute of Diabetes and Digestive and Kidney Diseases, the objective of the dataset is to predict whether or not a patient will get a Diabetes diagnosis, based on certain clinical measurements included in the dataset. The data resource is https://www.kaggle.com/uciml/pima-indians-diabetes-database.

For this project, we were asked to do the following:

Clean up your data set so that you can perform an EDA.

Perform EDA to identify opportunities to create new features.

Engineer new features, including at least three non-linear features (polynomial, log transformations, and/or interaction features) and at least three more new features that are not interactions or polynomial transformations.

Perform feature selection.

Fit four models to the data and tune at least two hyperparameters per model.

Decide on which evaluation metric you think is most appropriate for your project, evaluate how well your models perform, and identify your best model.

Use the outputs of your different models, along with your EDA work, to provide insight to your original question.

Explain how your model can be used to in the real world to solve a problem.

Data Overview
The Pima Indian data set contains 768 observations in the data, including eight potential variables and one predictor column called Outcome. Because all colums are the same length, it appears there are no missing data, but the data itself raises questions. For example, why is blood pressure information represented by just one half of the traditional measurement? We are told this is the diastolic pressure, which is the minimum pressure exerted on the walls of the arteries and/or can be thought of as the measurement during the resting or valve filling phase. Normal values are between 60-80 mm Hg, but this data includes values as high as 122 and as low as 0. The latter doesn't medically make sense. Further treatment of the data is necessary.

Having previewed the data statistics on the Kaggle site, the following are additional observations to explore:

Pregnancies: while possible, there are values as high as 17, which will be examined. There are 111 entries of 0, which is indeed possible.

Glucose: A two-hour, 75-gram oral glucose tolerance test (OGTT) is normally used to test for diabetes, which is usually interpreted as a dual measurement, including a fasting level of glucose. The average paired values (fasting, 2-hour) for diabetics is (126mg/dL or greater, 200 mg/dL or greater); for pre-diabetics is (100–125 mg/dL, 140–199 mg/dL); leaving non-diabetics in the ranges of (<100mg/dL, <140mg/dL). There are 5 values of 0 and other values as high as 200.

Blood Pressure: Normal values for diastolic blood pressure are between 60-80 mm Hg, but this data set includes values as high as 122 and as low as 0. Further research tells me that normal and elevated are <80 mm Hg. High blood pressure type 1 is 80-89 and high blood pressure type 2 is above 90. Hypertensive crisis is considered above 120. Severely low blood pressure (<<40) can deprive your body of enough oxygen to carry out its normal functions, leading to damage to your heart and brain. The zeros don't medically make sense, and probably represent that the data were not collected for these subjects.

Skin Thickness: According to "Chandra Selvi et al in IOSR Journal of Dental and Medical Sciences (IOSR-JDMS)2016, Skin fold thickness measurement provides an estimated size of the subcutaneous fat, which is the layer of subcutaneous tissue and composed of adipocytes. Subcutaneous fat is the major determinant of insulin sensitivity and has a strong association with insulin resistance. Normal is 23mm. We have 227 values of 0 (30% of the data set.)

Insulin: This measurement is likely a companion measurement to the Glucose test. I will explore options for using the two together. According to "Melmed S, et al 2011 Williams Textbook of Endocrinology. 12th ed.', blood sugar levels should be less than 80 mg/dl fasting and never rise above 110 or 120 mg/dl after one and two hour checks. Insulin should be less than 5 uIU/mL fasting and should never rise above 30 uIU/mL after one and two-hour checks.

BMI: The formula for BMI is 703 times weight in lbs/height in inches squared. The data set has 11 values of 0.

DiabetesPedigreeFunction: This is a measurement of genetic frequency, the calculation of which is unclear. As there are no values of 0, this variable will be explored for outliers and/or used as is.

Outcome: as a binary measurement, we can see that with 500 values of 0, there must be 268 values of 1.

Feature Engineering
I entered feature engineering with 760 subjects with 8 potential observations each, yielding an accuracy score through a logistic regression model of 75.8% and an F1 score of 75%.

My first feature to engineer is an HbA1c value, a well-established metric for diagnosing diabetes. The higher an A1C level, the higher risk of developing diabetes or complications of diabetes.

A normal A1C level is below 5.7 percent. A1C levels between 5.7 and 6.4 percent indicate prediabetes (also called impaired fasting glucose), which indicates high risk of developing diabetes in the future. An A1C level of 6.5 percent or higher indicates diabetes. An A1C level above 8 percent means that the diabetes is not well-controlled and the patient has a higher risk of developing complications of diabetes.

The American Diabetes Association’s Web site at www.diabetes.org/ag, provides a formula for this calculation: 28.7 x HbA1c — 46.7 = eAG (in mg/dl). This was used to calculate a new variable.

Other variables were pursued, such as interaction and polynomials, as well as binning existing variables.

Analysis and Conclusions
After reviewing 16 models, the best performing model for this analysis was the XG Boost. The F1 scores can be summarized as follows:

Logistic Regression: (0.667) K-Nearest Neighbors: (0.571, 0.575, 0.575, 0.600) Decision Tree: (0.541, 0.607, 0.772, 0.654) Random Forest: (0.614, 0.574, 0.571) XG Boost: (0.875, 0.860, 0.849 0.860)

The XG Boost model was the best performing model for this analysis. Through analysis of the classification errors and log loss, XG Boost in its second epoch delivered a strong predictive signal.