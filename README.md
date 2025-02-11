﻿# Lending Club Project  

This project was developed under the guidance of **Sumit Mittal** and is an implementation of my learnings in Apache Spark. The goal of the project is to calculate a **Loan Score** for customers based on historical and financial data.  

The project uses the dataset **accepted_2007_to_2018Q4.csv**, which is assumed to be ingested in real-time by an upstream team.  If you need the dataset , please add a comment with your email-id so I can provide you the same.

## Key Tables  

1. **Delinq Table**:  
   - Contains details about public records, bankruptcies, and inquiries.  

2. **Permanent Table Creation on Cleaned Data**:  
   - To support downstream teams, permanent tables are created based on cleaned data. These tables allow teams to query the data using SQL-like queries.  


## Loan Score Calculation  

The **Loan Score** is calculated based on the following factors:  
1. **Loan Payment History**: Repayment history of previous loans, if applicable.  
2. **Customer’s Financial Health**: Financial stability of the customer.  
3. **Loan Defaulter History**: Information on delinquencies, public records, bankruptcies, and inquiries.  

The **Loan Score** determines the likelihood of loan approval.  
- A **higher Loan Score** increases the chances of loan approval.  
- A **lower Loan Score** reduces the likelihood of approval.  

### Factors Affecting the Loan Score  

The Loan Score is influenced by three major factors, with their respective contributions:  
1. **Loan Repayment History (20%)**  
   - Based on:  
     - `last_payment`  
     - `total_payment_received`  

2. **Loan Defaulters History (45%)**  
   - Based on:  
     - `delinq_2years`  
     - `public_rec`  
     - `public_rec_bankruptcies`  
     - `inq_last_6mths`  

3. **Financial Health (35%)**  
   - Based on:  
     - `home_ownership`  
     - `loan_status`  
     - `funded_amount`  
     - `grade_points`  

### Identifying and Cleaning Bad Data  

- **Repeating Member IDs**:  
  - Bad data includes cases where multiple records exist for the same `member_id`.  
  - Ideally, there should only be one record per `member_id`.  
  - Records with repeating `member_id`s are identified and removed during data cleaning to ensure data quality.  
