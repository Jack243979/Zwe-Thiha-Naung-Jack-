#  Customer Churn Prediction | Olist E-Commerce Dataset

##  Project Overview
This project focuses on **predicting customer churn** for the Brazilian e-commerce platform **Olist** using **KNIME**, **SAS Viya**, and **Tableau**.  
The goal is to identify customers likely to churn and provide actionable recommendations to improve **customer retention** and **lifetime value**.
**Source**: See the full project scenerio 0[here](Project_Scenerio.md)

---

##  Dataset
**Source**: [Olist E-Commerce Public Dataset on Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce)

- 100k orders from 2016 to 2018
- 9 interrelated datasets
- 43 distinct columns

### **Key Datasets Used**
- `olist_customers_dataset.csv` - **Source**: [data](data/olist_customers_dataset.csv)
- `olist_orders_dataset.csv` - **Source**: [data](data/olist_orders_dataset.csv)
- `olist_order_items_dataset.csv`- **Source**: [data](data/olist_order_items_dataset.csv)
- `olist_order_payments_dataset.csv`- **Source**: [data](data/olist_order_payments_dataset.csv)

---

##  Data Preparation
Data preparation was performed using **KNIME**:
- **Data Cleaning** → Removed duplicates, null values, and outliers (IQR method).
- **Data Transformation** → One-hot encoding, region encoding, and datetime conversion.
- **Feature Engineering** → Generated 3 new features:
    - `delivered_estimated`
    - `purchase_approved_at`
    - `purchased_delivery`
- Final dataset: **19 features** → 8 categorical + 11 numerical.

---

##  Modeling
Four ML models were trained using **SAS Viya**:

| Model                 | Accuracy | Precision | Recall | F1 Score | Misclassification |
|----------------------|----------|-----------|--------|----------|--------------------|
| Logistic Regression  | 59.5%    | 59.9%     | 79.9%  | 68.4%    | 41.3%             |
| Gradient Boosting    | **70.0%**| **72.0%** | 75.0%  | **73.0%**| **29.9%**         |
| Decision Tree        | 68.2%    | 70.9%     | 72.4%  | 71.6%    | 31.7%             |
| SVM (Cuboid Kernel)  | 60.5%    | 60.7%     | **81.2%**| 69.4% | 39.5%             |

**Best Model** → **Gradient Boosting**  
**Best Simplicity** → **Decision Tree**

**Source**: See the full Modelling report [here](Model_Report.md)

---

##  Key Insights
- **Important Features**:
    - `freight_value`
    - `delivered_estimated`
    - `purchase_approved_at`
    - `purchased_delivery`
- High churn linked to:
    - High shipping costs 💸
    - Long delivery times ⏱️
    - Delayed payment approvals 🕒

---

##  Recommendations
- **Reduce Freight Value** → Optimize shipping costs or offer free-shipping promotions.
- **Improve Delivery Accuracy** → Align estimated vs actual delivery times.
- **Automate Payment Approvals** → Minimize processing delays.
- **Customer Retention Campaigns** → Target high churn-risk customers.

---

##  Tools & Technologies
- **KNIME** → Data preprocessing, feature engineering, and cleaning.
- **SAS Viya** → Model training, hyperparameter tuning, evaluation.
- **Tableau** → Data visualization and insights dashboard.
- **GitHub** → Version control and project management.

---

##  Project Structure
```bash
customer-churn-prediction/
├── data/                # Raw & processed datasets
├── notebooks/           # KNIME workflows
├── reports/             # PPTX and PDF reports
├── src/                 # Code for modeling (if applicable)
├── README.md
└── requirements.txt
