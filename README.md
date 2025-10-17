# 📘 Assignment – Imputation via Regression for Missing Data

## Name : Krishna Chaitanya
## Roll No: DA25M011

## 📂 Submission Contents
submission.ipynb → The single notebook that contains all code, visualisations, and explanations for this assignment.

## 📌 Overview
This assignment challenges you to apply linear and non-linear regression to impute missing values in a dataset. The effectiveness of your imputation methods will be measured indirectly by assessing the performance of a subsequent classification task, comparing the regression-based approach against simpler imputation strategies.

## Methodology 

### Introducing Missing At Random (MAR) on a clean dataset 

- As our given dataset was to try different imputation strategies, we introduced **MAR** by replacing 7% values in some numerical columns with **Nans**

### Imputation Strategy 1 
- Filling missing values with the **median** of the column.We choose the median over the mean because the median is more robust to outliers.

### Assumptions for below two Impuation Strategies below
- I couldn't get better info about remaining columns with null values, so I did this for these 2 imputation strategies
- I am dropping rows in training that contain null values of (marriage and pay_2)
- For test data, I am filling  the null values with the median.

### Imputation Strategy 2
- I chose **PAY_0** for filling the missing values and used a **Linear Regression model** to predict the missing values based on all other non-missing features.

### Imputation Strategy 3
- I chose **PAY_0** for filling the missing values and used a  **Non Linear Regression model ( K-Nearest Neighbours)** to predict the missing values based on all other non-missing features.

## Results 
| Model   | Accuracy | Recall | Precision | F1 Score |
|---------|----------|--------|-----------|----------|
| Model 1 | 0.691    | 0.641  | 0.378     | 0.476    |
| Model 2 | 0.693    | 0.645  | 0.387     | 0.484    |
| Model 3 | 0.692    | 0.645  | 0.387     | 0.484    |
| Model 4 | 0.685    | 0.636  | 0.363     | 0.462    |

## Conclusion and Final Recommendation

#### Imputation Strategies Vs ListWise Deletion

From the above results, we can see that the **imputation strategies** performs slightly better normal **listwise deletion**. This is because :

- In list wise deletion we are **deleting rows** which contains null values which lwads to a smaller dataset and.A smaller dataset provides less information for the model to learn so model doesnt generalize to new unseen data

- In our data we are reomving values of potentially **young customers** in dataset D so a model trained on this data performs well on older customers but performs poorly when it encounters younger customers as it hasnt seen any data on them which means we potentially making a biased model 

- But imputation stratgies instead of removing the values they tried to retained the original data distribution by filling in missing values and model trained on this data will generally outperform he model that was trained on a smaller, biased dataset.

- Hence **Model D** performs poorly when compared to A,B,C


#### Linear vs Non Linear Imputation 

- By observing the results ,Linear Regression Imputation (Model 2) performed the best.It slightly outperformed **Non-Linear Regression Imputation (Model 3)**.

- This suggest that relationship between **PAY_0** a(imputed feature) and other predictors is primarly **linear** which linear regression model is able capture effectively.

- On other hand **KNN** a non linear model may be couldnt able to find any significant non-linear patterns and its added complexity may have introduced noise leading to a slightly lower score.


#### Best Strategy For Handling Missing Data

- In this scenario **Linear Regression Imputation (Model 2)** is recommended as the best strategy.

- It has high **Recall** and **F1 score** which helps to detect positive cases more effectively.

- Linear imputation preserves data distribution while capturing the main linear relationships between features, avoiding the bias introduced by listwise deletion or the noise sometimes added by non-linear methods. 

- Hence Linear Regression Imputation is best for this dataset.
