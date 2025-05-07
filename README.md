import numpy as np
import pandas as pd

# Creating a larger dataset
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Emma', 'Frank', 'Grace', 'Henry', 'Isabella', 'Jack', 
             'Kelly', 'Liam', 'Mia', 'Noah', 'Olivia'],
    'Age': [25, 30, 22, 35, 28, 40, 27, 33, 29, 24, 31, 26, 34, 23, 32],
    'Salary': [50000, 60000, 45000, 70000, 55000, 80000, 52000, 65000, 58000, 47000, 
               61000, 53000, 72000, 46000, 69000],
    'Hours_Worked': [40, 45, 38, 50, 42, 48, 41, 46, 43, 39, 44, 40, 47, 37, 45],
    'Department': ['HR', 'IT', 'Marketing', 'Finance', 'HR', 'IT', 'Marketing', 'Finance', 'HR', 
                   'IT', 'Marketing', 'HR', 'Finance', 'IT', 'Marketing']
}

# Converting to DataFrame
df = pd.DataFrame(data)

# Basic analysis
print("Dataset Preview:")
print(df.head())
print("\n")

# Calculating mean, min, max for numerical columns
print("Basic Statistics:")
print("Average Age:", np.mean(df['Age']))
print("Average Salary:", np.mean(df['Salary']))
print("Minimum Hours Worked:", np.min(df['Hours_Worked']))
print("Maximum Hours Worked:", np.max(df['Hours_Worked']))
print("\n")

# Adding a new column for hourly rate
df['Hourly_Rate'] = df['Salary'] / (df['Hours_Worked'] * 52)  # Assuming 52 weeks/year
print("Dataset with Hourly Rate:")
print(df[['Name', 'Hourly_Rate']].round(2))
print("\n")

# Filtering employees with above-average salary
avg_salary = np.mean(df['Salary'])
high_earners = df[df['Salary'] > avg_salary]
print("Employees with Above-Average Salary:")
print(high_earners[['Name', 'Salary']])
print("\n")

# Grouping by age range
df['Age_Group'] = pd.cut(df['Age'], bins=[20, 25, 30, 35, 40], labels=['20-25', '26-30', '31-35', '36-40'])
age_group_stats = df.groupby('Age_Group', observed=False)[['Salary', 'Hours_Worked']].mean().round(2)
print("Average Salary and Hours by Age Group:")
print(age_group_stats)
print("\n")

# Grouping by department
dept_stats = df.groupby('Department')[['Salary', 'Hours_Worked']].mean().round(2)
print("Average Salary and Hours by Department:")
print(dept_stats)
