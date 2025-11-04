# 🏢 Salifort Motors Employee Turnover Predictor

### Data-Driven Strategies for Employee Retention

This project addresses the critical business challenge of **employee attrition** at Salifort Motors, a fictional automotive company. The goal is to build a highly accurate and reliable machine learning model to serve as an **Early Warning System (EWS)** for the HR department. By predicting which employees are **most likely to leave (Turnover = 1)**, the company can deploy targeted, proactive retention interventions, saving on recruitment costs and retaining institutional knowledge.

---

## 🔍 Key Findings & Exploratory Data Analysis (EDA)

The initial analysis revealed that employee turnover at Salifort Motors is driven not just by salary, but by a critical mix of **workload imbalance** and **low satisfaction**.

### 1. The Salary Factor (The Baseline)

<img width="1489" height="590" alt="image" src="https://github.com/user-attachments/assets/f528ed07-4211-4413-960a-5711ad61dd9e" />

The overall turnover rate is **16.6%** (1,991 employees out of 11,991 records). Compensation is the strongest single predictor: employees with a **Low Salary** leave at **4x the rate** of those with a High Salary.

### 2. The Workload Paradox

<img width="830" height="542" alt="image" src="https://github.com/user-attachments/assets/9cea4a8e-1e48-45f4-8887-1d6d9843f6b0" />

Turnover risk is high at both extremes of utilization:

* **Under-Utilized:** Employees with only **2 projects** have a **54.2%** turnover rate (indicating stagnation).
* **Optimal Zone:** Employees with **3 projects** have the lowest risk (~**1.1%** turnover).
* **Burnout Zone:** Employees with **6+ projects** face extremely high turnover (44.9% for 6 projects, 100% for 7 projects).

### 3. Burnout and The High-Performer Trap

<img width="845" height="542" alt="image" src="https://github.com/user-attachments/assets/6d26ed7c-4211-43ca-8df9-dd1c8ca7ced2" />

* **High Hours:** Departing employees work an average of **208 hours/month** (vs. 199 for stayers), confirming burnout.
* **The Trap:** A critical risk group involves **High-Performing** employees (**Evaluation $\ge$ 0.8**) who report **Low to Medium Satisfaction ($\le$ 0.5)**. These are highly valuable, unhappy employees who are likely seeking external opportunities.

---

## ⚙️ Methodology & Modeling

### Data Pipeline and Feature Engineering

The complete dataset of **11,991 unique records** was used.
1.  **Preprocessing:** Data cleaning, handling categorical variables (e.g., department and salary), and creating dummy variables.
2.  **Train/Test Split:** The dataset was divided into an **80% training set (~9,593 records)** and a **20% testing set (~2,398 records)** to ensure objective evaluation on unseen data.
3.  **Handling Imbalance:** Recognizing the significant class imbalance (~1:5 ratio), the project prioritized models robust to this challenge.

### Model Selection: XGBoost - The Champion Model

We compared three models, focusing on **Recall** as the primary metric. Maximizing Recall is crucial for an EWS because we must minimize **False Negatives** (employees who leave but the model failed to flag).

| Model         | Accuracy | Recall | Precision | F1-Score |
| :------------ | :------- | :----- | :-------- | :------- |
| Random Forest | 0.981    | 0.870  | 0.980     | 0.922    |
| **XGBoost** | **0.985**| **0.926**| **0.981** | **0.952**|

* **Model Chosen:** **XGBoost (Extreme Gradient Boosting)** provided the best balance, significantly improving **Recall** over Random Forest.

### Final Performance on Unseen Data

The XGBoost model is highly reliable:
* **Accuracy:** **98.5%** overall correct predictions.
* **Recall:** **0.926 (92.6%)**. The model successfully flags nearly 93% of all employees who actually leave.
* **Precision:** **0.981 (98.1%)**. When the model flags an employee, it is correct over 98% of the time, resulting in minimal "false alarms" for HR.
* **False Negatives:** The model only misclassified **37** actual departures out of the entire test set.

---

## 🚀 Strategic Recommendations

The model's predictions and feature importance scores translate directly into the following actionable HR strategies:

1.  **Proactive Workload Management:** Implement monitoring and alerts to prevent employees from falling into the 2-project (stagnation) or 6+-project (burnout) risk zones.
2.  **Targeted Compensation:** Immediately prioritize compensation adjustments for employees in the `salary_low` category, especially those showing other risk signs (like high hours).
3.  **High-Performer Retention:** Conduct immediate, targeted check-ins for high-evaluation employees whose satisfaction scores are dropping.
4.  **EWS Deployment:** Integrate model predictions into a simple HR dashboard to enable **personalized interventions** (e.g., counseling, flexible scheduling) before the employee decides to resign.

---

## 📁 Files in This Repository

* `HR_salifort_motors.ipynb`: The main Jupyter Notebook containing the data cleaning, EDA, feature engineering, model training, evaluation, and final model explanations.
* `Salifort Motors HR Analytics.pdf`: The final presentation summarizing the project scope, findings, and strategic recommendations for management.
