# 2024_CourseAssignment_EDA_ChurnModelingDataVisualization

# 📘 Overview

# ⚙️ Flow
## 1. Flowchart 1: Open Churn_Modelling.csv, examine the detailed attributes of the data, identify the attributes with missing values, and use box plots to illustrate their characteristics.

| Attribute Name | Has Missing Values | Attribute Meaning | Attribute Characteristics from Box Plot |
| :--- | :--- | :--- | :--- |
| `CustomerId` | No | Customer ID | It is a numeric attribute, the box plot is symmetric left and right, the data distribution is relatively even, with no special features. |
| `CredRate` | No | Customer Credit Level | It is a numeric attribute, where the outlier degree of the minimum value is higher than that of the maximum value. |
| `Geography` | No | Customer's Nationality | It is a categorical attribute, divided into France, Germany, and Spain. From the box plot, it can be seen that most customers are French. |
| `Gender` | No | Customer Gender | It is a categorical attribute, divided into Female and Male, with Male being more numerous. |
| `Age` | Yes | Customer Age | Ages are mainly concentrated between 30-45 years old. |
| `Tenure` | No | Years in Service | Years are mainly concentrated between 3-7 years. |
| `Balance` | No | Account Balance | Account balances are mainly between 90,000 and 130,000. |
| `Prod Number` | No | Product Quantity | Most are between 1 and 2. |
| `HasCrCard` | No | Has Credit Card | The number of people with credit cards is greater than those without. |
| `ActMem` | No | Is Active | The number of inactive people is greater than active ones. |
| `EstimatedSalary` | No | Estimated Salary | Salaries are mainly between 50,000 and 150,000. |
| `Exited` | No | Exited | There are far more satisfied customers who have not left than dissatisfied ones who have left. |

## 2. Flowchart 2 and 3 (Preprocessing)
### (1) Next, the following attributes in the data will be modified: {'CredRate' = 'CreditScore'; 'ActMem' = 'IsActiveMember'; 'Prod Number' = 'NumOfProducts'; 'Exited' = 'Churn'; }

The data table generated after renaming in the CSV file is as follows:

<img width="994" height="670" alt="image" src="https://github.com/user-attachments/assets/256edbd0-ff20-4238-a0a5-ab702bc91d5f" />

### (2) Set the Role of CustomerId to meta, and change the Role of Churn to target 
Use the Select Column tool to set CustomerId to meta, and Churn to target.

<img width="617" height="647" alt="image" src="https://github.com/user-attachments/assets/c1df6ba4-d046-48f0-b034-086ffbbac731" />

### (3) Convert HasCrCard and IsActiveMember to numeric
Use the Edit Domain tool to convert HasCrCard and IsActiveMember to numeric.

<img width="951" height="419" alt="image" src="https://github.com/user-attachments/assets/ac40aae5-477c-4752-bc51-034c1c53fbbb" />


### (4) Impute all missing values using average/most frequent 
Use the Impute tool to impute missing values using average/most frequent

<img width="752" height="727" alt="image" src="https://github.com/user-attachments/assets/7e47cf55-220c-42da-b9ab-da70362fe740" />

### (5) Transform Geography and Gender using one-hot encoding 
After selecting the attributes in the Continuize tool, set the original "use preset" to one-hot encoding.

<img width="865" height="785" alt="image" src="https://github.com/user-attachments/assets/561b7dfc-c035-431a-9423-b595dcc300a8" />

### (6) Check the current data (number of attributes, data types, Role). 
After the adjustments, you can use the Data Table to observe the data. The number of attributes should become 13, and Geography and Gender will each be split into two attributes due to one-hot encoding.

<img width="1196" height="186" alt="image" src="https://github.com/user-attachments/assets/0e02f990-b8e0-4812-b1c9-56269d47d9e9" />

## 3. Flowchart 2 (Model Prediction): Build a Logistic Regression model using all data, and use the model's coefficients to verify if the predictions for the first 50 records are correct.

### (1) The first step is to first build the logistic regression model and generate a corresponding table. This table will show the coefficients for each attribute, which will be used in the subsequent formula.

<img width="262" height="340" alt="image" src="https://github.com/user-attachments/assets/d2298ac9-5ddc-4433-b64f-007503d217c3" />

### (2) Next, create a Data Sampler to select 50 records.

<img width="273" height="511" alt="image" src="https://github.com/user-attachments/assets/87f7a936-953f-4b88-ae6c-84bd014370e7" />

### (3) Next, define the formula, which must incorporate the following equation:
p(y=1) = 1/(1 + exp(-(a1x1 + a2x2 + …… + c)))

<img width="664" height="546" alt="image" src="https://github.com/user-attachments/assets/24e7c5ea-bded-4774-a820-3b7f1ad9661e" />

### (4) Use the Data Table to print out the data.

<img width="621" height="730" alt="image" src="https://github.com/user-attachments/assets/8bfee879-c797-4b2d-936b-b74eabb71eed" />

### (5) To verify if it is correct, we need to use the Select Column tool to separately find the counts of True Positive, False Positive, True Negative, and False Negative. Among them, the total count of True Positive and True Negative represents the number of correct predictions by the model. As shown in the figure below, this model correctly predicted 38 out of the first 50 records.

<img width="1037" height="254" alt="image" src="https://github.com/user-attachments/assets/9a663274-4665-4966-9623-09c1024c9d4a" />

## 4. Flowchart 3 (Model Prediction): Using 10-fold cross-validation, find a set of SVM parameter combinations that can outperform the default Logistic Regression on CA. 

Below is a table listing the tested SVM parameter combinations and their CA values, where the default Logistic Regression's CA value is 0.790.
Initially, tune the Gamma value from small to large. After tuning a few times, it is found that with gamma at 0.1, the CA value can outperform the default Logistic Regression model.

<img width="1068" height="350" alt="image" src="https://github.com/user-attachments/assets/3b90cb84-7bbe-4134-86aa-9988e2d08b0e" />

<img width="1061" height="191" alt="image" src="https://github.com/user-attachments/assets/19030b40-93bc-41e5-b4f2-18a7e20fd78c" />

## 5. Flowchart 3 (Visualization): Fix the kernel function, vary different C values, and plot a scatter plot of the relationship between C values and the number of support vectors.

We can determine the number of Support Vectors by observing the instance count in the Data Table.
Next, after fixing the kernel function (using RBF here, with Gamma value set to 1), use Create Table to input the number of Support Vectors corresponding to different C values. The created Table and Scatter plot are shown in the following two figures.

<img width="1087" height="578" alt="image" src="https://github.com/user-attachments/assets/39c7b078-f47d-4558-ad91-5c8eb016040b" />












