# Gym Calories Prediction (SAS Viya)

Predicting **Calories_Burned** from demographic, physiological, and workout-related features using SAS Viya.  
This project compares multiple machine learning models across different dataset encodings and partition strategies to identify the best predictive and most interpretable approaches.

---

## 📜 Project Scenario
A gym operator wants to analyze fitness patterns and performance across different experience levels and understand which factors most influence **Calories_Burned**.

➡ **[Read the full project scenario](Project_Scenerio.md)**

---

## 📊 Model Report
The modeling process includes:
- Data preparation (encoded & non-encoded datasets)
- Four model techniques: Linear Regression, Decision Tree, Random Forest, Gradient Boosting
- Two partition strategies: 60/40 and 70/30
- Evaluation metrics: ASE (MSE) and RMSE
- Feature importance analysis
- Recommendations for accuracy-focused vs interpretability-focused use cases

➡ **[Read the full model report](Model_Report.md)**

---

## 🏆 Quick Results
- **Best predictive model:**  
  Gradient Boosting (non-encoded, 70/30 split)  
  ASE = **635**, RMSE = **25.2**
  
- **Best interpretable model:**  
  Linear Regression (encoded, 70/30 split)  
  ASE = **1606.3**, RMSE = **40.08**

---

## 🛠️ Tools & Techniques
- **Data Prep & Encoding:** SAS Viya, optional KNIME/Excel/Python
- **Modeling:** SAS Viya
- **Evaluation:** ASE (MSE), RMSE
- **Partitioning:** Simple random sampling with fixed random seed for reproducibility

---

## 🚀 How to Reproduce
1. Prepare the dataset (cleaning, optional encoding).
2. Partition into train/validation sets using both 60/40 and 70/30 splits.
3. Train the four models in SAS Viya.
4. Record validation ASE (MSE) and RMSE.
5. Compare models and select according to desired outcome (accuracy vs interpretability).

---

## 📄 License
MIT (or your chosen license)

