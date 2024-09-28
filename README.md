# London Ambulance Service Transparency Report Analysis (NHS Trust)

## Project Overview

This project analyzes the London Ambulance Service Transparency Report dataset, sourced from Kaggle, to gain insights into the organization's spending patterns and operational efficiency. The dataset contains detailed information on expenses, vendors, departments, and entities within the London Ambulance Service (NHS Trust). The project utilizes Python libraries like Pandas, NumPy, Matplotlib, and Seaborn for data manipulation, analysis, and visualization.

## Dataset

The dataset used for this analysis is the "London Ambulance Service Transparency Report" available on [Kaggle.](https://www.kaggle.com/datasets/imtkaggleteam/ambulance-transparency-report) It comprises NHS (National Health Service) data on spending over £25,000 in the London Ambulance Service NHS Trust.


## Project Goals

- **Descriptive Analysis:** Provide summary statistics, frequency counts, and distributions of expenses across various categories.
- **Exploratory Data Analysis:** Investigate trends and patterns in spending over time, by department, vendor, and expense type.
- **Vendor Analysis:** Identify top vendors and their contribution to overall expenses.
- **Departmental Analysis:** Analyze expense distribution across different departments.
- **Time-Series Analysis:** Explore monthly and yearly expense trends and forecast future expenses.
- **Outlier Detection:** Identify and analyze unusual or potentially problematic expenses.
- **Cost Reduction Opportunities:** Highlight areas where potential cost savings can be achieved.

## Methodology

### 1. Data Loading and Cleaning
```python
import pandas as pd
from google.colab import files

uploaded = files.upload()

df = pd.read_csv(next(iter(uploaded)))

df.head()
```

### 2.  Data Exploration and Preprocessing step-by-step

Code Walkthrough

```python
# Import necessary libraries
import pandas as pd

# Display basic information about the dataset
print("Dataset Info:")
df.info()

# Check for missing values
print("\nMissing Values:")
print(df.isnull().sum())

# Rename 'Unnamed: 5' to something more meaningful (e.g., 'Vendor')
df.rename(columns={'Unnamed: 5': 'Vendor'}, inplace=True)

# Display basic statistics for numerical columns
print("\nBasic Statistics:")
print(df.describe())

# Check the unique values in categorical columns to understand data better
categorical_columns = ['Department Family', 'Entity', 'Expense Type', 'Expense Area', 'Vendor']
for col in categorical_columns:
    print(f"\nUnique values in {col}:")
    print(df[col].unique())

# Check the first few rows after renaming
df.head()
```

## Exploratory Data Analysis (EDA)

- Total Expenses by Type

```python
expense_by_type = df.groupby('Expense Type')['Amount'].sum().sort_values(ascending=False)
print("\nTotal expenses by type:")
print(expense_by_type)
```

- Expenses Over Time

```python
expenses_over_time = df.groupby('Date')['Amount'].sum()
print("\nExpenses over time:")
print(expenses_over_time)
```

- Visualize Total Expenses by Entity

![image](https://github.com/user-attachments/assets/293c05a2-ae50-48ff-b51b-9d0a55421f67)


### 3. Descriptive Analysis

- Summary statistics for numerical columns

```python
print("Summary statistics for numerical columns:")
print(df.describe())

print("\nSummary statistics for categorical columns:")
print(df.describe(include=['object']))
```

- Frequency counts for categorical variables

```python
categorical_columns = ['Department Family', 'Entity', 'Expense Type', 'Expense Area']
for col in categorical_columns:
    print(f"\nFrequency count of {col}:")
    print(df[col].value_counts())
```

- Distribution of the Amount Column

  ![image](https://github.com/user-attachments/assets/895f2d75-174c-4d98-9af2-36ca61ce9312)

- Expense Distribution by Category (Expense Type, Entity)

![image](https://github.com/user-attachments/assets/9620a502-b097-490f-9cac-7be555b0d7e0)

![image](https://github.com/user-attachments/assets/d545f899-9fa5-466c-a9ee-2ce797e2c683)

- Correlation Between Numerical Variables

  ![image](https://github.com/user-attachments/assets/41662ad8-2b8b-4b30-9940-12daa715b923)

 - Time-Series Analysis

![image](https://github.com/user-attachments/assets/abdace34-5341-459c-bfed-df189ad861c2)

 - Top Vendors and Their Contribution to Expenses

   ![image](https://github.com/user-attachments/assets/0a9ebce0-da24-4edc-ba37-9e918ff3924f)

- Expense Distribution Across Different Departments

  ![image](https://github.com/user-attachments/assets/34e439d5-b988-4077-8301-0f1698e5eac2)

- Monthly Expense Trends

  ![image](https://github.com/user-attachments/assets/fa7a132c-ed03-42cb-b45c-5c01ea777150)

- Outlier Detection in Expenses

  ![image](https://github.com/user-attachments/assets/f6c4dabf-da87-4c17-b42d-727636cb72f5)

- Most Common Expense Areas

![image](https://github.com/user-attachments/assets/72994c6d-9924-46f8-a451-cc88350a710c)

- Year-over-Year (YoY) Expense Comparison

  ![image](https://github.com/user-attachments/assets/fd0c7ec3-70bb-49a6-a286-0e01735eb859)

- Cumulative Expense Over Time

  ![image](https://github.com/user-attachments/assets/8dba2ca5-40c5-4b99-9768-884880338379)


### Category-Wise Trend Analysis

```python
df.columns = df.columns.str.strip()

print(df.columns)

df['Date'] = pd.to_datetime(df['Date'], dayfirst=True)


df['Year-Month'] = df['Date'].dt.to_period('M')


expense_type_trends = df.groupby(['Year-Month', 'Expense Type'])['Amount'].sum().unstack().fillna(0)


for col in expense_type_trends.columns:
    expense_type_trends[col] = pd.to_numeric(expense_type_trends[col], errors='coerce')


import matplotlib.pyplot as plt

plt.figure(figsize=(12, 8))
expense_type_trends.plot(kind='line', marker='o', figsize=(12,8))
plt.title('Category-Wise Trend Analysis for Expense Type')
plt.xlabel('Year-Month')
plt.ylabel('Total Amount')
plt.xticks(rotation=45)
plt.grid(True)
plt.legend(title='Expense Type', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.tight_layout()
plt.show()
```

### Vendor-Specific Analysis

```python
df.columns = df.columns.str.strip()
vendor_expenses = df.groupby('Vendor')['Amount'].sum().sort_values(ascending=False)
top_vendors = vendor_expenses.head(10)
print(top_vendors)
```

### Vendor-Specific Trend Analysis (for Top Vendors)

![image](https://github.com/user-attachments/assets/b9c290d0-6e88-4c84-8bf8-0db2e1b4b954

### Variance and Standard Deviation of Expenses

---python
df['Amount'] = pd.to_numeric(df['Amount'], errors='coerce')


expense_variance = df['Amount'].var()
expense_std_dev = df['Amount'].std()


print(f"Variance of Expenses: {expense_variance:.2f}")
print(f"Standard Deviation of Expenses: {expense_std_dev:.2f}")
```

### Expense Per Entity Per Category

![image](https://github.com/user-attachments/assets/8372f0ec-2745-4532-8f9a-d2c77a4a3682)

### Expense Concentration

![image](https://github.com/user-attachments/assets/fd47385a-3310-41c5-9619-83b49edc1da1)


### Concentration by Expense Type

![image](https://github.com/user-attachments/assets/00704f43-d6fc-4eb5-bb73-da74c39f3069)

## Conclusion

This project provides a comprehensive analysis of the London Ambulance Service Transparency Report, offering insights into the organization's spending patterns and operational efficiency.
Use code with caution
I've included code snippets for key sections of your analysis and added placeholders for your visuals. Remember to replace these placeholders with the actual images generated during your analysis. I hope this revised overview is more helpful! Let me know if you have any other questions.
