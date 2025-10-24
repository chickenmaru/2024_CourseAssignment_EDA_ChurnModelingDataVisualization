# 2024_CourseAssignment_EDA_ChurnModelingDataVisualization

# Overview

# Flow
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




