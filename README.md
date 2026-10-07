# Telco Customer Churn Prediction

## About the project

This project is about predicting whether a telecom customer is likely to churn (leave the company) based on their account information, services, contract, charges, and other details.

I built this project to understand the complete machine learning workflow, from exploring the data to training and evaluating different classification models.

The main goal wasn't just to get the highest accuracy, but to understand **which model works best and which customer characteristics are related to churn**.

---

## Dataset

The dataset contains information about **7,043 telecom customers**.

Some of the features include:

- Customer tenure
- Contract type
- Internet service
- Monthly charges
- Total charges
- Payment method
- Online security
- Tech support
- Streaming services
- Senior citizen status

The target variable is:

**`Churn`**

- `Yes` → Customer left the company
- `No` → Customer stayed

There are 5,174 customers who stayed and 1,869 customers who churned, so the dataset is somewhat imbalanced.

---

## What I did

I followed a complete machine learning workflow:

1. Loaded and inspected the dataset
2. Explored numerical and categorical features
3. Checked the target variable and class imbalance
4. Investigated relationships between features and churn
5. Handled the `TotalCharges` data issue
6. Checked for missing values and duplicates
7. Removed the `customerID` column
8. Split the data into training and testing sets
9. Applied one-hot encoding to categorical variables
10. Standardized numerical features
11. Created a baseline model
12. Trained and compared five classification models
13. Used cross-validation to compare model performance
14. Tuned Logistic Regression
15. Tuned the prediction threshold
16. Evaluated the final model on the test set
17. Looked at Logistic Regression coefficients to understand the model

---

## Models tested

I compared the following models:

- Logistic Regression
- K-Nearest Neighbors (KNN)
- Decision Tree
- Random Forest
- Support Vector Machine (SVM)

### Model comparison

| Model | Accuracy | Precision | Recall | F1 |
|---|---:|---:|---:|---:|
| Logistic Regression | 80.55% | 65.72% | 55.88% | 60.40% |
| KNN | 76.37% | 55.27% | 57.49% | 56.36% |
| Decision Tree | 71.89% | 47.14% | 48.40% | 47.76% |
| Random Forest | 77.93% | 60.82% | 47.33% | 53.23% |
| SVM | 79.13% | 64.18% | 48.40% | 55.18% |

Based on the initial comparison and cross-validation, **Logistic Regression performed the best overall**, especially when looking at F1 score.

---

## Threshold tuning

The default classification threshold for Logistic Regression is 0.50.

I experimented with the threshold because, in a churn problem, missing a customer who is actually going to leave can be more costly than incorrectly flagging a customer.

Using cross-validation, the best threshold was approximately:

**0.33**

This increased the model's ability to identify customers who were actually going to churn.

### Final test results

Using the 0.33 threshold on the untouched test set:

| Metric | Result |
|---|---:|
| Accuracy | 76.15% |
| Precision | 53.80% |
| Recall | 71.93% |
| F1 Score | 61.56% |

The biggest improvement was recall.

The final model identified about **72% of the customers who actually churned**.

---

## Confusion Matrix

The final confusion matrix was:

```text
[[804 231]
 [105 269]]
```

This means:

- **804** customers were correctly predicted to stay
- **231** customers were predicted to churn but actually stayed
- **105** customers churned but were missed by the model
- **269** customers were correctly predicted to churn

The reduction in false negatives was one of the main reasons for lowering the classification threshold.

---

## What I learned from the model

One of the most interesting parts of the project was looking at the Logistic Regression coefficients.

Some of the features that pushed the prediction more toward churn were:

- Fiber optic internet service
- Month-to-month contracts
- Electronic check payment
- No online security
- No tech support

Features that pushed the prediction more toward staying included:

- Longer customer tenure
- Two-year contracts
- DSL internet service
- No paperless billing

These relationships don't necessarily mean that a feature **causes** churn. They show that the feature is useful for predicting churn in this dataset.

---

## Some observations from EDA

A few patterns stood out during the exploratory analysis:

- Customers with shorter tenure were more likely to churn.
- Month-to-month customers had much higher churn than customers on one- or two-year contracts.
- Customers using electronic checks showed higher churn.
- Customers without services such as online security and tech support tended to churn more.
- The dataset was imbalanced, with more customers staying than leaving.

These observations were also reflected in the final Logistic Regression model.

---

## Tools and libraries

The project was built using Python and the following libraries:

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook

---

## Project structure

```text
telco-customer-churn/
│
├── Telco_Customer_Churn.ipynb
├── README.md
├── .gitignore
└── data/
```

---

## How to run the project

Clone the repository and open the Jupyter Notebook:

```bash
git clone <your-repository-url>
cd telco-customer-churn
```

Then open:

```text
Telco_Customer_Churn.ipynb
```

Make sure the dataset is available in the expected location before running the notebook.

---

## Final thoughts

This was one of my projects for learning and understanding the machine learning workflow end-to-end.

The main thing I took away from this project is that **accuracy isn't always the most useful metric**, especially when the goal is to identify customers who may churn.

In this case, lowering the prediction threshold allowed the model to catch more potential churners, although it also increased the number of false positives.

The project also helped me understand the difference between simply training a model and actually evaluating, tuning, and interpreting one.
