# Credit Risk Analysis: Reducing Loan Defaults through Pattern Recognition
## About 
The main goal of this project is to study Nova Bank’s loans to figure out why some people fail to pay back their loans. The analysis looks for the main factors that cause defaults and suggests practical steps the bank can take to reduce losses.

The main thing we’re looking at is whether a loan was paid back or not (loan_status = 0 for paid, 1 for default).

Baseline risk: Overall, about 22 out of 100 loans are not paid back, so all findings are compared to this averag

### About Dataset
1. Personal/Demographic Information
<pre>
client_ID - Unique identifier for each borrower
person_age - Age of the borrower
person_income - Annual income
gender - Gender of the borrower
marital_status - Marital status
education_level - Education level attained
country - Country of residence
state - State of residence
city - City of residence
city_latitude - Latitude coordinate of city
city_longitude - Longitude coordinate of city
</pre>

2. Employment Information
<pre>
person_emp_length - Employment length in years (has missing values)
employment_type - Type of employment
person_home_ownership - Home ownership status (rent, own, mortgage, etc.)
</pre>
3.Loan Characteristics
<pre>
loan_amnt - Loan amount requested
loan_intent - Purpose of the loan (debt consolidation, education, medical, etc.)
loan_grade - Credit grade assigned to the loan
loan_int_rate - Interest rate on the loan (has missing values)
loan_percent_income - Loan amount as percentage of income
loan_status - Target variable (0 = paid, 1 = default)
</pre>
4. Credit History & Behavior
<pre>
cb_person_default_on_file - Whether person has previous default on file
cb_person_cred_hist_length - Length of credit history in years
open_accounts - Number of open credit accounts
credit_utilization_ratio - Credit card utilization ratio
past_delinquencies - Number of past delinquent payments
</pre>

5. Engineered Financial Ratios
<pre>
debt_to_income_ratio - Total debt payments relative to income
loan_to_income_ratio - Loan amount relative to annual income
</pre>

## Data Quality Assessment
Before analysis, the dataset was evaluated for quality issues:

Missing Values: Identified columns with missing data .
Duplicates: Checked for duplicates
Data Types: Ensured all variables were stored in appropriate formats.

## Key Insights
### 1. How does the size of a loan compared to a person’s income affect their chances of defaulting?
   
People are much more likely to default when they borrow a large portion of their income. Most customers who repay their loans borrow about 10–15% of their yearly income,
while those who default usually borrow around 25%. To reduce future losses, Nova
bank should avoid giving loans over 20–25% of a person’s income, or at least review these applications very carefully

<img width="900" height="390" alt="image" src="https://github.com/user-attachments/assets/057a9b78-29c0-4a46-bb2a-13f55626450f" />


### 2. Does having too much existing debt make someone more likely to default on a new loan?
people who already spend a large part of their income on debts are more likely to default. Customers who default usually have a debt-to-income (DTI) ratio of around 41%, 
while those who repay their loans have a DTI of about 31%.

Therefore, Nova Bank should flag or reject loan applications from people with a DTI above 40%, because most borrowers cannot handle additional debt beyond this point.

<img width="900" height="390" alt="image" src="https://github.com/user-attachments/assets/ad9685cb-4093-455e-aedb-a9b8a3fcfbff" />

### 3. Does charging higher interest rates lead to more customers failing to pay back their loans?

When interest rates go above 13%, the risk of default increases sharply. For loans above 16%, over 60% of borrowers fail to repay. This means Nova bank is losing more money than it earns
from the high interest.

Therefore, Nova bank should seriously limit or stop giving loans with interest rates above 16%, because the high default rate outweighs any extra income from interest
<img width="900" height="390" alt="image" src="https://github.com/user-attachments/assets/e7f06d7e-2a2f-43fe-93ce-ab851cf5a2e9" />

### 4. How does the size of the loan affect the chance that a customer will default?

Larger loans fail more often. Loans over $20,000 are especially risky, with about 1 in 3 borrowers not repaying. Since these loans cause the biggest losses, 
Nova bank should be stricter with loans over $15,000 and limit loans above $20,000

<img width="900" height="390" alt="image" src="https://github.com/user-attachments/assets/b20fbc38-77db-4db3-a3ce-923dc87f05be" />


### 5. Which groups of customers and loan reasons are causing the biggest losses?

The heatmap shows where the biggest problems come from. The worst losses happen when people with very poor credit (Grades D–G) take loans for Debt Consolidation or Medical reasons.
These loans fail so often that the bank loses a lot of money.

Therefore, Nova Bank should stop giving loans to people in credit grades D–G for Debt Consolidation or Medical purposes, because the failure rate is too high.

<img width="535" height="593" alt="image" src="https://github.com/user-attachments/assets/52109c79-7223-4098-ad55-3c7316c7fbe6" />

### 6. Which numbers tell us most clearly if a borrower is likely to default?
The biggest risks come from how much people are borrowing compared to their income, so using Loan Percent Income is the clearest way to judge who might default

<img width="900" height="586" alt="image" src="https://github.com/user-attachments/assets/0a016333-5c69-482f-9e44-7a0983838b7a" />


### 7. Which credit grades contribute most to loan defaults and financial losses?

<pre>
            default_rate   volume  risk_exposure
loan_grade                                      
A               0.099564  10777.0     10202525.0
B               0.162760  10451.0     19120425.0
C               0.207340   6458.0     13579600.0
D               0.590458   3626.0     22800100.0
E               0.644191    964.0      7826925.0
F               0.705394    241.0      2496875.0
G               0.984375     64.0      1098925.0
</pre>

Grades A–C: Lower default rates (10–21%) and large number of loans. Most defaults are smaller relative to the total volume.

Grades D–G: Extremely high default rates (59–98%), even if there are fewer loans. These grades are causing the largest losses per loan, especially D and E.

Grade G: Almost everyone defaults (98%), but there are only 64 loans. Still, even a small number of these loans can be risky.

Therefore,  Nova bank should be very careful lending to Grades D–G, as these grades account for the largest risk exposure, even though there are fewer loans in these groups

## Recommendations
Loan Size vs. Income: Loans above 20–25% of a person’s income are high-risk. Carefully review or limit these applications.

Existing Debt (DTI): Borrowers with DTI > 40% are likely to default. Flag or decline these loans.

Interest Rates: Loans above 16% interest have very high default rates (>60%). Limit or stop lending to this group.

Large Loans: Loans over $15,000 should face stricter checks; reduce loans above $20,000 to prevent large losses.

Credit Grade & Loan Purpose: The highest losses occur when poor-credit borrowers (Grades D–G) take loans for Debt Consolidation or Medical reasons. Stop lending in these segments.

Predictive Metrics: Loan Percent Income (LPI) is the clearest predictor of default. Use this metric to assess borrower risk.

Credit Grade Risk: Grades D–G contribute the most to financial losses. Be cautious with loans to these borrowers.










