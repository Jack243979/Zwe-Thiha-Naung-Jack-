<h1>(1). Data Preparation</h1>
<h2>Column Names</h2>
<p>As a first step for data cleaning, the names of the dimensions in the dataset are transformed into the names that would fit into Sas Viya.</p>
<img width="550" height="400" alt="Screenshot 2025-08-13 165340" src="https://github.com/user-attachments/assets/be980809-7a47-42b4-89c9-e6d6d62aaa0d" />
<h2>Outliers and Duplicates</h2>
<img width="300" height="500" alt="Screenshot 2025-08-13 165559" src="https://github.com/user-attachments/assets/4798f37f-8730-4bf8-9d89-5a34e3f6d934" />
<img width="339" height="500" alt="Screenshot 2025-08-13 171236" src="https://github.com/user-attachments/assets/59572d51-489d-4a89-8a2f-fac45fda66f3" />
<p>There is no null value and unacceptable outliers in the dataset. (Outliers difference for BMI is 0.01. So that’s not a concern case).<br>
When removing duplicate rows using Duplicate Row Filter node in Knime, the data row changes from 4865 to 973, which is indicating that the original dataset contains a lot of duplicated rows.
</p>
<h2>Data Encoding</h2>
<p>Knime node: Rule Engine<br>
Male to 0 and Female to 1<br>
Workout type: <br>
Yoga -> 1, Strength -> 2, Cardio -> 3, HIIT -> 4.<br>
Workout type is encoded by rank based on the amount of calories burnt, referencing the following article. (by theory)<br>
  https://www.fitnessfirst.com.au/get-there/how-many-calories-are-you-really/
</p>
<h2>Knime Workflow</h2>
<img width="1367" height="676" alt="Screenshot 2025-08-15 021412" src="https://github.com/user-attachments/assets/56dbf327-d439-427f-b7d4-598dd91e0f93" />
<h2>Feature selection</h2>
<h3>By Theory:</h3>
<p><i>BMI, Gender, Age, Workout Type, Session hours, BPM </i></p>
<p>https://www.coospo.com/blogs/knowledge/calories-burned-by-heart-rate-understanding-the-connection (reference)<br>
https://tyemedical.com/blog/what-affects-how-many-calories-you-burn-6-factors-to-consider/ (reference)
</p>
<h3>Correlation Matrix:</h3>
<img width="1953" height="1153" alt="Screenshot 2025-08-13 200419" src="https://github.com/user-attachments/assets/53fcae02-9a57-4a1b-88b3-068f869ba248" />
<p><u>Features selected from correlation matrix:</u><br>
<i>Workout_Frequency(0.5762) , Water_Intake (0.3569), Session_Duration (0.9081), Fat_Percentage (-0.5976), Experience_level(0.6941).</i> 
</p>
<h3>Multicollinearity check:</h3>
<p>Since Experience level is highly correlated with <i>workout_frequency(0.8371), session_duration(0.7648) and fat_percentage(-0.6544)</i>, remove it from model to get a better model performance.</p>
<h3>Finalized Features: </h3>
<p><i>BMI, Age, Gender, Workout_Type, Session_Duration, Avg_BPM, Water_Intake, Fat_Percentage and Experience_level.</i>
Total <b>6 numerical features and 3 categorical features</b>.
</p>
<h1>(2). Modelling</h1>
<h2>Objective</h2>
<p>The objective of the modelling phase is to predict <i><b>Calories_Burned</b></i> using demographic, physiological, and workout-related features. Multiple algorithms were tested in SAS Viya to identify the best-performing model.</p>
<h2>Modelling Approach</h2>
I initially created two versions of the dataset for modelling approach. In the first, categorical variables such as <i>Gender, Workout_Type and Experience_Level</i> were encoded into numerical values to suit algorithms requiring numeric input. In the second, I kept the categorical variables in their original form to test models that can process them directly. This allowed me to compare performance and see if encoding had a noticeable effect on prediction accuracy for target variable.
<h2>Partitioning</h2>
<p>Before doing any modelling techniques, I partitioned the dataset into training dataset and validation dataset into <i>(60%,40%) and (70%,30%)</i> .<br>
<b>Random number seed</b> box is checked to maintain the data consistency in comparing different ML models.
</p>
<h2>Modelling Techniques</h2>
<i><b>The following models are the demos of non-encoded dataset with 60/40 Partition ID</b></i>
<h3>Linear Regression</h3>
<b>: Simple baseline model to capture linear relationships.</b>
<img width="2479" height="1199" alt="image" src="https://github.com/user-attachments/assets/09dccb00-3b92-4055-8f5c-e139ed0f9d67" />
Average squared error (ASE) of the Model: <b>1863.9</b>
<h3>Decision Tree</h3>
<b>: Easy-to-interpret rules for feature relationships.</b>
<img width="2466" height="1219" alt="Screenshot 2025-08-14 212641" src="https://github.com/user-attachments/assets/136717d1-0d4e-4dc7-990d-63be54711aaf" />
<b>Parameter Tuning</b><br>
Changing the maximum branches in the model from 2(default) to 4 improves the model since ASE changes from 7.1K to 5.4K.<br>
Average squared error (ASE) of the Model: <b> 5446.8 </b>
<h3>Random Forest</h3>
<b>: Ensemble approach to reduce overfitting and improve accuracy.</b>
<img width="2437" height="1202" alt="Screenshot 2025-08-14 212204" src="https://github.com/user-attachments/assets/4fbb3faa-ac3e-40b2-8268-1f85687b693c" />
<b>Parameter Tuning</b><br>
Increasing the maximum branches in the model 2(default) makes the model worse. And even though reducing the leaf size from 5 technically reduces ASE, the difference between validation ASE and training ASE increases (overfitting). <br>
Average squared error (ASE) of the Model: <b>8657.2</b>
<h3>Gradient Boosting</h3>
<b>: Boosted ensemble method for handling complex patterns.</b>
<img width="2477" height="1215" alt="Screenshot 2025-08-14 213651" src="https://github.com/user-attachments/assets/8f04e74a-97a1-4832-b000-9e0f5aa2c136" />
<b>Parameter Tuning</b><br>
Even though increasing the maximum depth of the model slightly reduces the Validation ASE from 758 to 715, the gap between validation ASE and training ASE increases from 449 to 541. To avoid overfitting, the maximum depth of 5 is chosen. <br>
Average squared error (ASE) of the Model: <b>758</b>
<h3>Model Comparison</h3>
The performance of four predictive models: L<b>inear Regression, Decision Tree, Random Forest, and Gradient Boosting,</b> was evaluated using <b>two dataset variations (encoded and non-encoded categorical variables) across <b>two partition strategies</b> (60/40 and 70/30 train/validation splits). Each model’s performance was assessed using <b>Mean Squared Error (MSE or ASE) and Root Mean Squared Error (RMSE)</b> on the validation set using 9 features across every model to ensure a fair and consistent comparison.
<img width="2460" height="1218" alt="Screenshot 2025-08-14 215450" src="https://github.com/user-attachments/assets/56e8d824-c696-4de5-a844-e528aadc942a" />
<b>Model comparison of non-encoded dataset with 60/40 Partition ID.</b><br>
  ---
  
## 📊 Results

### Model comparison — **non-encoded** dataset (60/40)
| Model            | Dataset Type            | ASE (MSE) | RMSE  |
|------------------|-------------------------|-----------|-------|
| Linear Regression| Non-encoded (60/40)     | 1863.9    | 43.2  |
| Decision Tree    | Non-encoded (60/40)     | 5446.8    | 73.8  |
| Random Forest    | Non-encoded (60/40)     | 8657.2    | 93.04 |
| Gradient Boosting| Non-encoded (60/40)     | **758**   | **27.5** |

### Model comparison — **non-encoded** dataset (70/30)
| Model            | Dataset Type            | ASE (MSE) | RMSE  |
|------------------|-------------------------|-----------|-------|
| Linear Regression| Non-encoded (70/30)     | 1715.9    | 41.4  |
| Decision Tree    | Non-encoded (70/30)     | 5386.4    | 73.4  |
| Random Forest    | Non-encoded (70/30)     | 7454.8    | 86.3  |
| Gradient Boosting| Non-encoded (70/30)     | **635**   | **25.2** |

### Model comparison — **encoded** dataset (60/40)
| Model            | Dataset Type         | ASE (MSE) | RMSE  |
|------------------|----------------------|-----------|-------|
| Linear Regression| Encoded (60/40)      | **1637.6**| **40.5** |
| Decision Tree    | Encoded (60/40)      | 5936.3    | 77.04 |
| Random Forest    | Encoded (60/40)      | 8124.9    | 90.1  |
| Gradient Boosting| Encoded (60/40)      | 953.5     | 30.9  |

### Model comparison — **encoded** dataset (70/30)
| Model            | Dataset Type         | ASE (MSE) | RMSE  |
|------------------|----------------------|-----------|-------|
| Linear Regression| Encoded (70/30)      | **1606.3**| **40.08** |
| Decision Tree    | Encoded (70/30)      | 5936.8    | 77.1  |
| Random Forest    | Encoded (70/30)      | 7744.6    | 88    |
| Gradient Boosting| Encoded (70/30)      | **696.3** | **26.4** |

<h2>Final Optimal Models</h2>
Based on the model comparison results, <b>Gradient Boosting with the non-encoded dataset and a 70/30 partition </b>achieved the lowest validation <b>ASE (635) and RMSE (25.2)</b>, making it the optimal model for <b> predicting Calories Burned.
</b>
<img width="2478" height="1203" alt="Screenshot 2025-08-15 010938" src="https://github.com/user-attachments/assets/527a11b1-3b65-4250-a882-68934448895d" />
For <b>interpretability purposes</b>, the <b>best-performing Linear Regression model</b> was selected from the comparisons. The model trained on the encoded dataset with a 70/30 partition achieved the lowest validation ASE (1606.3) and RMSE (40.08) among all Linear Regression runs, making it the most suitable choice for generating <b>explainable insights on the factors influencing Calories Burned.</b>
<img width="2471" height="1218" alt="Screenshot 2025-08-15 011122" src="https://github.com/user-attachments/assets/6bee79a5-6557-4037-97e7-bddbb4b57d34" />

## (3) Evaluation

### 3.1 Feature Importance
- **Session_Duration (hours)** showed the strongest relationship with **Calories_Burned** across models.
- **Age**, **Fat_Percentage**, and **Avg_BPM** appeared as important variables in **every** model.
- **Workout_Frequency** and **Workout_Type** were influential in **Linear Regression** and **Random Forest**, but were less (or not) important in **Decision Tree** and **Gradient Boosting**.
- **Avg_BPM**—despite only a modest correlation with the target (r = **0.3397**) from theory—proved crucial for predictive performance.  
  - Removing **Avg_BPM** caused validation **ASE** to jump from **635** to **10,650.5**, underscoring the importance of theory-guided feature selection.

### 3.2 Impact of Encoding Categorical Variables
- For **Gradient Boosting** and **Random Forest**, encoding had **minimal effect**, since tree ensembles natively handle categorical splits.
- For **Linear Regression**, encoding provided a **small performance gain** (e.g., ASE improved from **1863.9** to **1637.6**).
- For **Decision Trees**, performance differences were **negligible** between encoded and non-encoded datasets—encoding is not strictly necessary in SAS Viya for tree-based methods.

### 3.3 Trade-offs: Accuracy vs. Interpretability
- **Gradient Boosting** achieved the **lowest ASE/RMSE** overall and is the **most accurate** model. However, as a black-box ensemble it is **less interpretable**, which may limit its usefulness when clear explanations are required by gym trainers/operators.
- **Linear Regression** was **slightly less accurate** but offers **transparent coefficients** and straightforward interpretation of each feature’s effect on **Calories_Burned**—preferable when stakeholder insight is a priority.

### 3.4 Model Recommendations
- **Prediction-focused applications:**  
  - **Use:** **Gradient Boosting**  
  - **Config:** **Non-encoded dataset**, **70/30** train/validation split (lowest observed ASE **= 635**, RMSE **= 25.2**).
- **Insight & explanation:**  
  - **Use:** **Linear Regression**  
  - **Config:** **Encoded dataset**, **70/30** train/validation split (best LR run ASE **= 1606.3**, RMSE **= 40.08**).

> Summary: Choose **Gradient Boosting** when accuracy is paramount; choose **Linear Regression** when interpretability for decision-making is the main objective.


