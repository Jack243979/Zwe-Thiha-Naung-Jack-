(1). Data Preparation
Column Names
As a first step for data cleaning, the names of the dimensions in the dataset are transformed into the names that would fit into Sas Viya.
 <img width="402" height="333" alt="image" src="https://github.com/user-attachments/assets/0a23e5fc-97ac-4e72-a837-85725e877c83" />

Outliers and Duplicates
    
There is no null value and unacceptable outliers in the dataset. (Outliers difference for BMI is 0.01. So that’s not a concern case).
When removing duplicate rows using Duplicate Row Filter node in Knime, the data row changes from 4865 to 973, which is indicating that the original dataset contains a lot of duplicated rows.
Data Encoding
Knime node: Rule Engine
Male to 0 and Female to 1
Workout type: 
Yoga -> 1, Strength -> 2, Cardio -> 3, HIIT -> 4.
Workout type is encoded by rank based on the amount of calories burnt, referencing the following article. (by theory)
https://www.fitnessfirst.com.au/get-there/how-many-calories-are-you-really/
Knime Workflow
    
Feature selection
By Theory:
BMI, Gender, Age, Workout Type, Session hours, BPM 
https://www.coospo.com/blogs/knowledge/calories-burned-by-heart-rate-understanding-the-connection(reference)
https://tyemedical.com/blog/what-affects-how-many-calories-you-burn-6-factors-to-consider/(reference)
Correlation Matrix:
 
Features selected from correlation matrix:
Workout_Frequency(0.5762) , Water_Intake (0.3569), Session_Duration (0.9081), Fat_Percentage (-0.5976), Experience_level(0.6941). 
Multicollinearity check:
Since Experience level is highly correlated with workout_frequency(0.8371), session_duration(0.7648) and fat_percentage(-0.6544), remove it from model to get a better model performance.
Finalized Features: 
BMI, Age, Gender, Workout_Type, Session_Duration, Avg_BPM, Water_Intake, Fat_Percentage and Experience_level.
Total 6 numerical features and 3 categorical features.
(2). Modelling
Objective
The objective of the modelling phase is to predict Calories_Burned using demographic, physiological, and workout-related features. Multiple algorithms were tested in SAS Viya to identify the best-performing model.
Modelling Approach
I initially created two versions of the dataset for modelling approach. In the first, categorical variables such as Gender, Workout_Type and Experience_Level were encoded into numerical values to suit algorithms requiring numeric input. In the second, I kept the categorical variables in their original form to test models that can process them directly. This allowed me to compare performance and see if encoding had a noticeable effect on prediction accuracy for target variable.
Partitioning
Before doing any modelling techniques, I partitioned the dataset into training dataset and validation dataset into (60%,40%) and (70%,30%).
Random number seed box is checked to maintain the data consistency in comparing different ML models.
 
Modelling Techniques
The following models are the demos of non-encoded dataset with 60/40 Partition ID
Linear Regression
: Simple baseline model to capture linear relationships.
 
Average squared error (ASE) of the Model: 1863.9
Decision Tree
: Easy-to-interpret rules for feature relationships.
 
Parameter tuning - changing the maximum branches in the model from 2(default) to 4 improves the model since ASE changes from 7.1K to 5.4K.
Average squared error (ASE) of the Model: 5446.8
Random Forest
: Ensemble approach to reduce overfitting and improve accuracy.
 
Parameter tuning - increasing the maximum branches in the model 2(default) makes the model worse. And even though reducing the leaf size from 5 technically reduces ASE, the difference between validation ASE and training ASE increases (overfitting). 
Average squared error (ASE) of the Model: 8657.2
Gradient Boosting
: Boosted ensemble method for handling complex patterns.
 
Parameter tuning - even though increasing the maximum depth of the model slightly reduces the Validation ASE from 758 to 715, the gap between validation ASE and training ASE increases from 449 to 541. To avoid overfitting, the maximum depth of 5 is chosen.
Average squared error (ASE) of the Model: 758
Model Comparison
The performance of four predictive models: Linear Regression, Decision Tree, Random Forest, and Gradient Boosting, was evaluated using two dataset variations (encoded and non-encoded categorical variables) across two partition strategies (60/40 and 70/30 train/validation splits). Each model’s performance was assessed using Mean Squared Error (MSE or ASE) and Root Mean Squared Error (RMSE) on the validation set using 9 features across every model to ensure a fair and consistent comparison.
 

Model comparison of non-encoded dataset with 60/40 Partition ID. (above ss and below table)
Model	Dataset Type	ASE (MSE)	RMSE
Linear Regression	Non-encoded (60/40)	1863.9	43.2
Decision Tree	Non-encoded (60/40)	5446.8	73.8
Random Forest	Non-encoded (60/40)	8657.2	93.04
Gradient Boosting	Non-encoded (60/40)	758	27.5

Model comparison of non-encoded dataset with 70/30 Partition ID
Model	Dataset Type	ASE (MSE)	RMSE
Linear Regression	Non-encoded (70/30)	1715.9	41.4
Decision Tree	Non-encoded (70/30)	5386.4	73.4
Random Forest	Non-encoded (70/30)	7454.8	86.3
Gradient Boosting	Non-encoded (70/30)	635	25.2

Model comparison of encoded dataset with 60/40 Partition ID
Model	Dataset Type	ASE (MSE)	RMSE
Linear Regression	Encoded (60/40)	1637.6	40.5
Decision Tree	Encoded (60/40)	5936.3	77.04
Random Forest	Encoded (60/40)	8124.9	90.1
Gradient Boosting	Encoded (60/40)	953.5	30.9

Model comparison of encoded dataset with 70/30 Partition ID
Model	Dataset Type	ASE (MSE)	RMSE
Linear Regression	Encoded (70/30)	1606.3	40.08
Decision Tree	Encoded (70/30)	5936.8	77.1
Random Forest	Encoded (70/30)	7744.6	88
Gradient Boosting	Encoded (70/30)	696.3	26.4

Final Optimal Models
Based on the model comparison results, Gradient Boosting with the non-encoded dataset and a 70/30 partition achieved the lowest validation ASE (635) and RMSE (25.2), making it the optimal model for predicting Calories Burned.
 
For interpretability purposes, the best-performing Linear Regression model was selected from the comparisons. The model trained on the encoded dataset with a 70/30 partition achieved the lowest validation ASE (1606.3) and RMSE (40.08) among all Linear Regression runs, making it the most suitable choice for generating explainable insights on the factors influencing Calories Burned.
 
(3). Evaluation
Features important
Session_Duration (hours) is the feature that were strongly related to calorie expenditure.
Age, Fat_Percentage and Avg_BPM are the three features that were variables importance in every model.
Even though Workout_Frequency and Workout_Type are important variables in Linear Regression and Random Forest models, they are less or no important in other two models.
Surprisingly, Avg_BPM, the feature taken by Theory and poorly correlated with the target (0.3397), is found out that the key feature driving the model performance. Removing it from the model rapidly changes ASE from 635 to 10650.5. This is indicating the importance of feature selection by Theory.
Impact of Encoding Categorical Variables
Encoding categorical data generally had minimal effect on Gradient Boosting Random Forest models, as these techniques can handle categorical splits internally. However, the impact of encoding showed a slight model performance in Linear Regression model (for example, ASE changed from 1863.9 to 1637.6). In Decision Trees, performance differences were negligible between encoded and non-encoded datasets, confirming that encoding is not strictly necessary for tree-based methods in SAS Viya.
Recommendation
Trade-offs Between Accuracy and Interpretability
The Gradient Boosting model achieved the lowest ASE and RMSE overall, making it the most optimal model among four models. However, it operates as a black-box ensemble method, making the model less suitable when clear interpretability is required. In this case, I assume that for gym trainers and operators, clear interpretation is required even though the model is the best. 
On the other hand, the Linear Regression model, while slightly less accurate, offers transparent coefficients that allow visible interpretations of how each feature influences Calorie_Burned. This reason makes the model more suitable for stakeholders such as gym operators who require explainable insights over purely predictive performance.
Model Recommendations
So, I want to recommend that if the model is for prediction-focused applications, Gradient Boosting model can be used. And if the model is for insight and explanation, Linear Regression is recommended.
For prediction-focused applications -> Gradient Boosting with non-encoded dataset with 70/30 Partition ID.
For insight and explanation -> Linear Regression with encoded dataset with 70/30 Partition ID.

