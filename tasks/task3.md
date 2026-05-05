# Task 3: DataFrame Exploration (EDA Basics)

## Task

You are given a dataset in Excel format. Perform basic exploration and analysis using pandas.

## Input Data

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from google.colab import drive
drive.mount('/content/gdrive', force_remount=True)

df = pd.read_excel('/content/data.xlsx', decimal=',')
```

Dataset: [dataset_3_4.xlsx](https://github.com/ice-avalanche/ds_course_en/blob/4258662412a23bc60866c7545920f8f4deb6628a/datasets/dataset_3_4.xlsx)

## 1. Basic overview

* Check structure of the dataset

```python
df.________()        # method that shows info (columns, types, missing)

df.________()        # method that shows summary statistics

df.________          # attribute that returns (rows, columns)
```

## 2. Explore columns

* Get column names

```python
df.________          # attribute with all column names
```

* Count unique rows (all columns)

```python
df.________()        # method that counts unique row combinations
```

## 3. Work with a specific column

* Get unique values from Age

```python
df["Age"].________()   # method to get unique values
```

## 4. Basic statistics

* Calculate statistics for Age and Salary

```python
print(
    df["Age"].________(),      # max value
    df["Age"].________(),      # min value
    df["Age"].________(),      # average (mean)
    df["Age"].________(),      # median

    df["Salary"].________(),   # max value
    df["Salary"].________(),   # min value
    df["Salary"].________(),   # average (mean)
    df["Salary"].________()    # median
)
```

## 5. Data types

* Convert HireDate to datetime

```python
df["HireDate"] = pd.to_datetime(
    df["HireDate"],
    errors="________"   # string to ignore incorrect values
)
```

## 6. Missing values

* Check missing values per column

```python
df.________().________()   # first check NaN, then sum
```

* Calculate percentage of missing values

```python
df.________().________()   # first check NaN, then mean
```

## 7. Filtering

* Select employees older than 30

```python
df[df["________"] > 30]   # column with age
```

* Select employees with Salary > 5000

```python
df[df["________"] > 5000]   # column with salary
```

## 8. Sorting

* Sort by Salary (descending)

```python
df.________("Salary", ascending=________)   # sort function + False for descending
```

## 9. New features

* Create column: salary_per_age

```python
df["salary_per_age"] = df["________"] / df["________"]   # salary / age
```

## 10. Simple visualization

* Plot distribution of Salary

```python
df["Salary"].________(bins=20)   # histogram method

plt.show()
```

* Plot Age vs Salary

```python
plt.________(df["Age"], df["Salary"])   # scatter plot function

plt.show()
```

## 11. Group analysis

* Average Salary by Age

```python
df.groupby("________")["________"].________()   # group by age, take salary, calculate mean
```
