# Amazon-Sales-Report-Analysis-Using-Python
Here’s a README template for your Amazon sales data analysis project. You can adjust any sections to fit your specific style or requirements.

---

# Amazon Sales Data Analysis

## Project Overview

This project focuses on analyzing sales data from Amazon using Python libraries such as NumPy, Pandas, Matplotlib, and Seaborn. The primary objective is to clean the data, perform exploratory data analysis (EDA), and generate meaningful insights through visualizations. 

The dataset contains details about sales, sizes, categories, shipment statuses, fulfillment methods, and more. By cleaning the data and analyzing key features, the report highlights important trends and patterns related to Amazon sales.

 Key Components of the Project
# 1. Data Understanding and Cleaning

The dataset is loaded using Pandas. Initial exploration includes viewing the structure, data types, and shape of the dataset to identify potential issues such as missing values and incorrect data types.

```python
import pandas as pd

df = pd.read_csv("Amazon Sale Report.csv")
print(df.head())
df.info()
```

Columns such as "New" and "PendingS", which contain many null values, are dropped.

```python
df = df.drop(["New", "PendingS"], axis=1)
df.info()
```

Missing values in columns like 'fulfilled-by' are filled with the default value 'Easy Ship'.

```python
df.fillna({'fulfilled-by': 'Easy Ship'}, inplace=True)
```

Further handling includes converting data types (e.g., converting `ship-postal-code` to integers and `Date` to datetime format) and dropping rows where `ship-postal-code` is missing.

### 2. Exploratory Data Analysis (EDA)

Descriptive statistics provide insights into numerical and categorical data distributions.

```python
df.describe()
df.describe(include='object')
```

Visualizations are used extensively to understand relationships and trends in the data.

### Visualizations

- **Size Analysis**: A bar plot visualizes the most popular sizes purchased by customers. The analysis reveals that M-size is the most bought size.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  ax = sns.countplot(x='Size', data=df, hue='Size', palette='viridis')
  plt.show()
  ```

- **Category Analysis**: A plot is generated to understand the distribution of product categories, showing a preference for T-shirts.

- **B2B Buyers**: A pie chart illustrates the proportion of B2B buyers versus regular retail customers, indicating that 99.3% of buyers are retailers.

  ```python
  B2B_Check = df['B2B'].value_counts()
  plt.pie(B2B_Check, labels=B2B_Check.index, autopct='%1.1f%%')
  plt.show()
  ```

- **State Distribution**: A bar plot displays the distribution of buyers across different states, with Maharashtra having the largest customer base.

  ```python
  sns.countplot(data=df, x='ship-state', palette='viridis')
  plt.xticks(rotation=90)
  plt.show()
  ```

### Additional Insights

The analysis includes a scatter plot to visualize the relationship between product categories and sizes.

```python
x_data = df['Category']
y_data = df['Size']

plt.scatter(x_data, y_data)
plt.xlabel('Category')
plt.ylabel('Size')
plt.title('Scatter Plot')
plt.show()
```

Another pie chart analyzes fulfillment methods, revealing that most orders are fulfilled by Amazon.

```python
a1 = df['Fulfilment'].value_counts()
fig, ax = plt.subplots()
ax.pie(a1, labels=a1.index, autopct='%1.1f%%', radius=0.7, wedgeprops=dict(width=0.6))
ax.set(aspect="equal")
plt.show()
```

### Top 10 States by Buyers

The top 10 states with the most buyers are plotted, showing that Maharashtra has the highest customer base.

```python
top_10_state = df['ship-state'].value_counts().head(10)
sns.countplot(data=df[df['ship-state'].isin(top_10_state.index)], x='ship-state', palette='viridis')
plt.xticks(rotation=45)
plt.show()
```

## Conclusion

The analysis of Amazon sales data reveals several key insights:
- The business has a significant customer base in Maharashtra state.
- It mainly serves retailers.
- Most orders are fulfilled by Amazon.
- There is high demand for T-shirts, with M-Size being the preferred choice among buyers.
