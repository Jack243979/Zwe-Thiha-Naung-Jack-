# 📊 Model Evaluation Report — Customer Churn Prediction

## 🔹 Overview
This report presents the **modeling process**, **evaluation metrics**, and **recommendations** for the **Customer Churn Prediction Project** using the **Olist E-Commerce dataset**.  
Four machine learning models were trained and evaluated using **SAS Viya**.

---
## 🔹 Data Preparation
Knime Workflow for Data Cleaning, Transformation and Feature Engeering.

<img width="1720" height="559" alt="Screenshot 2025-08-17 193408" src="https://github.com/user-attachments/assets/a9a3a781-f0e4-4454-9bff-39153464ed11" />

**Source**: [data](data/olist_customers_dataset.csv)

---
## 🔹 Models Evaluated
I tested four supervised classification models:

- **Logistic Regression**
- **Gradient Boosting**
- **Decision Tree**
- **Support Vector Machine (SVM)**
 <img width="1956" height="1184" alt="Screenshot 2025-08-17 232429" src="https://github.com/user-attachments/assets/7bf6e6f7-3b83-4ed4-8749-6eb8d13e12e3" />
**Gradient Boosting**
<img width="1960" height="1182" alt="Screenshot 2025-08-17 233912" src="https://github.com/user-attachments/assets/789bd83a-face-45e0-b703-ae4a7e37d933" />
**Decision Tree**
<img width="1960" height="1180" alt="Screenshot 2025-08-17 234624" src="https://github.com/user-attachments/assets/adb58e01-f03b-420c-9568-d22a5b31b179" />
**Support Vector Machine (SVM)**
<img width="1958" height="1179" alt="Screenshot 2025-08-17 232055" src="https://github.com/user-attachments/assets/1a00bbfe-e520-4e9c-a339-9b6cdf5e026f" />
**Logistic Regression**

---

## 🔹 Evaluation Metrics

| Model                | Accuracy | Precision | Recall | F1 Score | Misclassification |
|---------------------|----------|-----------|--------|----------|--------------------|
| Logistic Regression | 59.5%    | 59.9%     | 79.9%  | 68.4%    | 41.3%             |
| Gradient Boosting   | **70.0%**| **72.0%** | 75.0%  | **73.0%**| **29.9%**         |
| Decision Tree       | 68.2%    | 70.9%     | 72.4%  | 71.6%    | 31.7%             |
| SVM (Cuboid Kernel) | 60.5%    | 60.7%     | **81.2%** | 69.4% | 39.5%             |

---

## 🔹 Key Findings

### 1. **Best Model — Gradient Boosting**
- Achieved the **highest accuracy** and **F1-score**.
- Balanced trade-off between **precision** and **recall**.
- Captures churners effectively while minimizing false positives.

### 2. **Alternative — Decision Tree**
- Slightly lower accuracy than Gradient Boosting but offers **high interpretability**.
- Recommended if model explainability is critical.

### 3. **High-Recall Use Case — SVM**
- Achieves the **highest recall (81.2%)**.
- Suitable when the priority is to **catch as many churners as possible**, even if false positives increase.

---

## 🔹 Feature Importance (From Gradient Boosting)
Top 4 features influencing churn prediction:

| Rank | Feature                | Description                                    | Impact |
|------|------------------------|-----------------------------------------------|--------|
| 1    | `freight_value`        | Shipping cost paid by customer               | High shipping cost → higher churn risk |
| 2    | `delivered_estimated`  | Estimated vs actual delivery date difference | Longer delays → higher churn |
| 3    | `purchase_approved_at` | Time taken to approve payment                | Slow approvals → dissatisfaction |
| 4    | `purchased_delivery`   | Actual delivery duration                     | Longer deliveries → higher churn |

---

## 🔹 Recommendations

### **Business Actions**
- **Reduce Freight Value** → Offer discounts or free shipping thresholds.
- **Improve Delivery Timelines** → Align estimated and actual delivery dates.
- **Automate Payment Approvals** → Reduce approval processing delays.
- **Retention Campaigns** → Target customers flagged as “high churn risk.”

### **Next Steps**
- Deploy the **Gradient Boosting** model in production.
- Set up **real-time churn scoring** for each customer.
- Build a **dashboard** to monitor churn risk over time.

---

## 📌 Conclusion
The **Gradient Boosting** model is the most suitable for this project due to its **high accuracy, balanced performance, and interpretability of feature importance**.  
By leveraging these insights, Olist can **reduce churn** and **improve customer satisfaction**.

---
