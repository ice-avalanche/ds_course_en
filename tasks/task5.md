# Task 5: Exploratory Data Analysis (EDA)

## Task

You are given a dataset. Perform a full exploratory data analysis using pandas, matplotlib, and seaborn.

## Input Data

```python id="0g6q2a"
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("data.csv")
```

Dataset: [dataset_5_6.xlsx](https://github.com/ice-avalanche/ds_course_en/blob/990ff6309a8b80157efffea39d24ef117f0b25f6/datasets/dataset_5_6.xlsx)

## 1. First look

* Display first and last rows

```python id="3k4y1q"
df.________()   # method to show first rows (head)
df.________()   # method to show last rows (tail)
```

* Check shape and columns

```python id="8m7c5n"
df.________        # attribute with (rows, columns)
df.________        # attribute with column names
```

## 2. Data overview

* Get general info

```python id="4r2j8t"
df.________()   # method that shows info (types, nulls)
```

## 3. Summary statistics

* Numeric columns

```python id="5p9z6b"
df.________()   # method for numeric summary (describe)
```

* All columns

```python id="7v1l2d"
df.________(include="________")   # include all columns ("all")
```

## 4. Missing values

* Count missing values

```python id="9t8q4x"
df.________().________()   # first isna(), then sum()
```

* Percentage of missing

```python id="6c3h1w"
df.________().________()   # first isna(), then mean()
```

* Visualize missing values

```python id="2f7n9k"
sns.________(df.isna(), cbar=False)   # heatmap

plt.show()
```

## 5. Handling missing values

* Fill missing values in Age

```python id="1z5m8p"
df["Age"] = df["Age"].________(df["Age"].________())   # fillna(mean)
```

* Drop rows with missing values

```python id="3d6k2y"
df = df.________()   # dropna
```

## 6. Duplicates

* Check duplicates

```python id="8p1v7n"
df.________().________()   # duplicated().sum()
```

* Remove duplicates

```python id="5y3q4r"
df = df.________()   # drop_duplicates
```

## 7. Data types

* Convert date column

```python id="2n6w8x"
df["date"] = pd.to_datetime(df["date"], errors="________")   # "coerce"
```

## 8. Distributions

* Histogram of Salary

```python id="4b9k1c"
df["Salary"].________(bins=30)   # hist

plt.show()
```

* Seaborn version

```python id="7x2r5m"
sns.________(df["Salary"], bins=30)   # histplot

plt.show()
```

## 9. Outliers

* Boxplot

```python id="6m3v2a"
sns.________(x=df["Salary"])   # boxplot

plt.show()
```

* Filter extreme values

```python id="9q8n1b"
df[df["Salary"] < df["Salary"].________(0.99)]   # quantile
```

## 10. Categorical analysis

* Count categories

```python id="3k7r2p"
df["city"].________()   # value_counts
```

* Plot categories

```python id="8v1y6c"
df["city"].________().plot(kind="________")   # value_counts + "bar"

plt.show()
```

## 11. Relationships

* Scatter plot

```python id="2c5m8z"
plt.________(df["Age"], df["Salary"])   # scatter

plt.show()
```

* Seaborn scatter

```python id="5t9x3q"
sns.________(x="Age", y="Salary", data=df)   # scatterplot

plt.show()
```

## 12. Correlation

* Compute correlation

```python id="6y2b4n"
df.________(numeric_only=True)   # corr
```

* Heatmap

```python id="1r8p6k"
sns.________(df.corr(numeric_only=True), annot=True)   # heatmap

plt.show()
```

## 13. Group analysis

* Average Salary by city

```python id="9d4m7s"
df.groupby("________")["________"].________()   # city, Salary, mean
```

* Plot result

```python id="4k1w9z"
df.groupby("________")["________"].mean().plot(kind="________")   # city, Salary, bar

plt.show()
```

## 14. Segment analysis

* Create high_salary feature

```python id="7p3c5x"
df["high_salary"] = df["Salary"] > ________   # threshold like 60000
```

* Analyze by segment

```python id="2m8v1q"
df.groupby("________")["Age"].________()   # high_salary, mean
```

## 15. Time-based analysis

* Extract year and month

```python id="6n4y2t"
df["year"] = df["date"].dt.________   # year
df["month"] = df["date"].dt.________  # month
```

* Plot trend

```python id="5q7k3r"
df.groupby("________")["Salary"].mean().plot()   # group by month or year

plt.show()
```
