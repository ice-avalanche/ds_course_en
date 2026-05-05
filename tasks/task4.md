# Task 4: Data Visualization

## Task

Using the dataset from Task 3, build several types of visualizations to explore the data.

## Input Data

```python id="l2f7sx"
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_excel('/content/data.xlsx')

df["HireDate"] = pd.to_datetime(df["HireDate"], errors="coerce")
```

Dataset: [dataset_3_4.xlsx](https://github.com/ice-avalanche/ds_course_en/blob/4258662412a23bc60866c7545920f8f4deb6628a/datasets/dataset_3_4.xlsx)

## 1. Line plot

* Plot trend of average Salary over time (by year or month)

```python id="z1k9wp"
df["year"] = df["HireDate"].dt.________

df.groupby("________")["________"].mean().plot()

plt.title("Salary over time")
plt.show()
```

## 2. Scatter plot

* Plot relationship between Age and Salary

```python id="q8t2mv"
plt.scatter(
    df["________"], 
    df["________"]
)

plt.xlabel("Age")
plt.ylabel("Salary")

plt.show()
```

## 3. Histogram

* Plot distribution of Salary

```python id="n4p8rl"
plt.hist(
    df["________"], 
    bins=________
)

plt.title("Salary Distribution")

plt.show()
```

## 4. Bar chart

* Plot average Salary by Age or Category

```python id="x3k7qb"
df.groupby("________")["________"].mean().plot(kind="________")

plt.title("Average Salary by Group")

plt.show()
```

## 5. Boxplot

* Show Salary distribution by Category or Age

```python id="t9y6vd"
sns.boxplot(
    x=df["________"],
    y=df["________"]
)

plt.title("Salary Distribution by Group")

plt.show()
```
