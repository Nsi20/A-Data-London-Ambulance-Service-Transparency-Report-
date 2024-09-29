# London Ambulance Service Transparency Report Analysis (NHS Trust)

## Project Overview

This project analyzes the London Ambulance Service Transparency Report dataset, sourced from Kaggle, to gain insights into the organization's spending patterns and operational efficiency. The dataset contains detailed information on expenses, vendors, departments, and entities within the London Ambulance Service (NHS Trust). The project utilizes Python libraries like Pandas, NumPy, Matplotlib, and Seaborn for data manipulation, analysis, and visualization.

## Dataset

The dataset used for this analysis is the "London Ambulance Service Transparency Report" available on [Kaggle.](https://www.kaggle.com/datasets/imtkaggleteam/ambulance-transparency-report) It comprises NHS (National Health Service) data on spending over £25,000 in the London Ambulance Service NHS Trust.

## Tools Used 

### Programming Language:

Python: This entire analysis is performed using Python, a versatile language for data analysis and visualization.

### Libraries:

- Pandas: Used for data manipulation, cleaning, and analysis. It provides data structures like DataFrames for working with tabular data.
- NumPy: Used for numerical computations, especially array operations.
Matplotlib: Used for creating static, interactive, and animated visualizations.
-Seaborn: Built on top of Matplotlib, Seaborn provides a higher-level interface for creating informative and attractive statistical graphics.

### Specific Tools and Techniques:

- Data Loading: google.colab.files is used to upload data to the Colab environment.
- Data Cleaning: Pandas functions are used for renaming columns, converting data types, and handling missing values.
- Data Aggregation: groupby() function in Pandas is used to group data by different categories (e.g., expense type, vendor).
- Data Visualization: Various plot types from Matplotlib and Seaborn are used, including bar charts, line charts, heatmaps, and box plots.
- Descriptive Statistics: Pandas functions like describe() are used for calculating summary statistics.
- Time Series Analysis: Datetime functionalities in Pandas are used to analyze monthly and yearly trends.
- Rolling Average: rolling() function in Pandas is used to calculate moving averages for smoothing time series data.
- Pareto Analysis: Customized code is used to calculate and visualize the cumulative percentage of expenses and vendors.
- Anomaly Detection: Statistical methods are applied to identify outliers based on standard deviation and thresholds.
  
### Google Colab Environment:

The project leverages the Google Colab platform, which provides a cloud-based environment for running Python code and includes pre-installed libraries for data analysis. [Google Colaboratory](https://colab.google/)

## Project Goals

- **Descriptive Analysis:** Providing summary statistics, frequency counts, and distributions of expenses across various categories.
- **Exploratory Data Analysis:** Investigating trends and patterns in spending over time, by department, vendor, and expense type.
- **Vendor Analysis:** Identifying top vendors and their contribution to overall expenses.
- **Departmental Analysis:** Analyzing expense distribution across different departments.
- **Time-Series Analysis:** Exploring monthly and yearly expense trends and forecast future expenses.
- **Outlier Detection:** Identifying and analyzing unusual or potentially problematic expenses.
- **Cost Reduction Opportunities:** Highlighting areas where potential cost savings can be achieved.

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

### Vendor-Specific Trend Analysis (for Top Vendors)
![image](https://github.com/user-attachments/assets/e95d31a4-9cd0-4856-95ba-1291cb4ecd7e)

![image](https://github.com/user-attachments/assets/d5acaba4-a146-45b9-94d9-bb880a79bc43)

![image](https://github.com/user-attachments/assets/33f08e18-3884-49ee-9c57-292a52b8880e)

![image](https://github.com/user-attachments/assets/796eb9e0-b880-424a-bd1c-9af1a72d9a75)

![image](https://github.com/user-attachments/assets/23c6de85-0f00-4bf6-8743-8be5cee13301)

![image](https://github.com/user-attachments/assets/07113724-a36d-4afb-84a9-19fd880771fd

![image](https://github.com/user-attachments/assets/c46ec1a7-f867-4b67-99eb-7985920793b9)

![image](https://github.com/user-attachments/assets/e96ba28b-7165-49a9-99cf-5b059a280bdf)

![image](https://github.com/user-attachments/assets/a7fb7782-1212-4fd2-8b09-aa46b1be5491)

![image](https://github.com/user-attachments/assets/6006cbba-fa17-4812-864c-2f5a75d16fd8)

![image](https://github.com/user-attachments/assets/03b259a9-1666-49bf-82ce-218ac662ac4a)

# Key Findings of this project

## Expense Distribution and Trends

- Highest Expenses: The London Ambulance Service has significant spending on Telecommunications, Medical and Surgical Supplies, and Professional Services. These categories represent potential areas for cost reduction.

- Top Vendors: A few vendors (Vendor A, Vendor B, etc.) account for a large portion of the total expenses. These could be considered for negotiation or alternative sourcing.

- Monthly Trend: Expenses generally increase over time, indicating potential inflationary or operational growth factors.
  
- Departmental Differences: Certain departments (Emergency Medical Services, Administration) have higher spending than others. Further analysis can focus on their specific needs and resource allocation.
  
- Expense Frequency: Expenses occur more frequently on weekdays and during specific months, reflecting operational patterns and seasonality.

### Potential Cost-Saving Opportunities:

- Recurring Large Expenses: Analyze top vendors and recurring large expenses. This could lead to possibilities for negotiation with the vendors or the discovery of alternative sources, potentially resulting in savings.
  
- Telecommunications and Vendor A: These areas have significant spending, making them prime targets for optimization.
Analysis Techniques:

### Pareto Analysis: 

- Identified the 80/20 rule: a few vendors and departments account for most expenses.
  
- Time-Based Analysis: Monthly expenses analysis revealed general trends and potential seasonality.
  
- Cross-Departmental Comparisons: Comparison across departments provides context for resource allocation and potential cost variations.


# My Recommendations for the London Ambulance Service

Following a comprehensive analysis of the organization's transparency report data, i recommend the following actions to optimize spending, enhance operational efficiency, and promote data-driven decision-making:

### Cost Reduction and Optimization

Strategic Vendor Management: I recommend actively engaging with top vendors to negotiate more favourable rates or explore alternative vendors to potentially reduce costs. This approach can significantly impact the budget, particularly for recurring large expenses.

### Telecommunications Optimization:

A review of the telecommunications expenses is warranted to identify opportunities for cost savings. This may involve optimizing current plans, reducing overall usage, or exploring alternative communication technologies.

### Outlier Investigation:

I advise investigating the identified expense outliers to determine if they are legitimate or require corrective action. Addressing these outliers could prevent potential financial losses and improve budget accuracy.

### Recurring Expense Reduction:
I recommend implementing cost-saving measures for recurring expenses in specific categories. This may include strategies such as bulk purchasing, energy efficiency initiatives, or process improvements to minimize costs over time.

## Operational Efficiency

### Resource Optimization: 
I recommend analyzing expense distribution across departments to identify potential areas for resource optimization. This analysis can inform decisions about reallocating funds to areas with higher needs or greater impact on operational efficiency.

### Proactive Expense Monitoring:
I suggest establishing a system for regular monitoring of monthly and yearly expense trends. This proactive approach can help identify potential issues early on and enable timely adjustments to budgets and operations.

### Transparency Enhancement: 
I encourage continued publication and enhancement of the transparency report. This practice fosters accountability, promotes public trust, and provides valuable insights into the organization's spending patterns.

## Data-Driven Decision Making

- Data-Informed Budgeting: I recommend leveraging the insights from this analysis to inform future budget planning and resource allocation decisions. This data-driven approach can lead to more strategic and effective budget management.

- Predictive Modeling: I advise exploring more advanced forecasting techniques to predict future expenses. This capability can support proactive budget adjustments and resource planning to better manage financial resources.

- Continuous Data Analysis: I recommend implementing a system for ongoing data collection and analysis. This continuous monitoring will enable the organizations to track performance, identify emerging trends, and make data-driven decisions for continuous improvement.

- By adopting these recommendations, the London Ambulance Service can leverage data to make strategic decisions, optimize spending, and enhance operational efficiency for the benefit of the organization and the public it serves.

## Conclusion

This project comprehensively analyses the London Ambulance Service Transparency Report, offering insights into the organization's spending patterns and operational efficiency.

## Future Work: 
Further investigation is needed to explore the specific cost drivers for the top expense categories and evaluate the potential for negotiation with major vendors. Predictive models could be developed to forecast future expenses and enhance budget planning. Comparing spending patterns with other ambulance services could provide valuable benchmarks for performance improvement.

### Limitations:
This analysis was limited by the available data in the transparency report. More granular data, including details about individual transactions and service utilization, would enhance future analysis.
