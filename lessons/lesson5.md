# Lesson 5: Exploratory Data Analysis (EDA)

## 1. Setup

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

Load data:

```python
df = pd.read_csv("data.csv")
```

## 2. First look at data

```python
df.head()
df.tail()
```

Shape:

```python
df.shape
```

Columns:

```python
df.columns
```

Data types:

```python
df.dtypes
```

## 3. Data overview

```python
df.info()
```

Key points:

* number of rows
* missing values
* column types

## 4. Summary statistics

```python
df.describe()
```

Include all:

```python
df.describe(include="all")
```

## 5. Missing values

Check:

```python
df.isna().sum()
```

Percentage:

```python
df.isna().mean()
```

Visual check:

```python
sns.heatmap(df.isna(), cbar=False)
plt.show()
```

## 6. Handling missing values (basic)

Drop:

```python
df = df.dropna()
```

Fill:

```python
df["age"] = df["age"].fillna(df["age"].mean())
```

## 7. Duplicates

Check:

```python
df.duplicated().sum()
```

Remove:

```python
df = df.drop_duplicates()
```

## 8. Data types correction

```python
df["date"] = pd.to_datetime(df["date"])
df["salary"] = df["salary"].astype(float)
```

## 9. Distributions

Numeric columns:

```python
df["salary"].hist(bins=30)
plt.show()
```

Seaborn:

```python
sns.histplot(df["salary"], bins=30)
plt.show()
```

## 10. Outliers

Boxplot:

```python
sns.boxplot(x=df["salary"])
plt.show()
```

Filter extreme values:

```python
df[df["salary"] < 100000]
```

## 11. Categorical analysis

```python
df["city"].value_counts()
```

Plot:

```python
df["city"].value_counts().plot(kind="bar")
plt.show()
```

## 12. Relationships

Scatter:

```python
plt.scatter(df["age"], df["salary"])
plt.show()
```

Seaborn:

```python
sns.scatterplot(x="age", y="salary", data=df)
plt.show()
```

## 13. Correlation

```python
df.corr(numeric_only=True)
```

Heatmap:

```python
sns.heatmap(df.corr(numeric_only=True), annot=True)
plt.show()
```

## 14. Group analysis

```python
df.groupby("city")["salary"].mean()
```

Plot:

```python
df.groupby("city")["salary"].mean().plot(kind="bar")
plt.show()
```

## 15. Segment analysis

```python
df["high_salary"] = df["salary"] > 60000

df.groupby("high_salary")["age"].mean()
```

## 16. Feature inspection

Check distribution by group:

```python
sns.boxplot(x="city", y="salary", data=df)
plt.show()
```

## 17. Time-based analysis

If date exists:

```python
df["date"] = pd.to_datetime(df["date"])

df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
```

Aggregation:

```python
df.groupby("month")["salary"].mean().plot()
plt.show()
```

## 18. Real EDA workflow

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# load data
df = pd.read_csv("data.csv")

# 1. OVERVIEW

print("Shape:", df.shape)
print("\nColumns:", df.columns.tolist())

df.info()

print("\nData types:\n", df.dtypes)

# sample
df.head(3)

# 2. MISSING VALUES

missing_count = df.isna().sum()
missing_ratio = df.isna().mean()

missing_df = pd.DataFrame({
    "missing_count": missing_count,
    "missing_ratio": missing_ratio
}).sort_values("missing_ratio", ascending=False)

print("\nMissing values:\n", missing_df)

# visualization
plt.figure(figsize=(8, 4))
sns.heatmap(df.isna(), cbar=False, cmap="viridis")
plt.title("Missing Values Heatmap")
plt.show()

# 3. DISTRIBUTIONS

plt.figure(figsize=(8, 5))

plt.hist(
    df["salary"],
    bins=30,
    color="steelblue",
    edgecolor="black",
    alpha=0.8
)

plt.title("Salary Distribution", fontsize=14)
plt.xlabel("Salary")
plt.ylabel("Frequency")
plt.grid(axis="y", linestyle="--", alpha=0.6)

plt.show()

# with KDE
plt.figure(figsize=(8, 5))

sns.histplot(
    df["salary"],
    bins=30,
    kde=True,
    color="skyblue",
    edgecolor="black"
)

plt.title("Salary Distribution (with KDE)")
plt.show()

# 4. RELATIONSHIPS

plt.figure(figsize=(8, 5))

sns.scatterplot(
    x="age",
    y="salary",
    data=df,
    color="orange",
    s=70,
    alpha=0.7,
    edgecolor="black"
)

plt.title("Age vs Salary")
plt.xlabel("Age")
plt.ylabel("Salary")
plt.grid(True, linestyle="--", alpha=0.5)

plt.show()

# with regression line
plt.figure(figsize=(8, 5))

sns.regplot(
    x="age",
    y="salary",
    data=df,
    scatter_kws={"alpha": 0.5},
    line_kws={"color": "red", "linewidth": 2}
)

plt.title("Age vs Salary (with trend)")
plt.show()

# 5. GROUP ANALYSIS

grouped = df.groupby("city")["salary"].agg(["mean", "median", "count"])
print("\nGrouped stats:\n", grouped)

# bar plot
plt.figure(figsize=(8, 5))

plt.bar(
    grouped.index,
    grouped["mean"],
    color="teal",
    edgecolor="black"
)

plt.title("Average Salary by City")
plt.xlabel("City")
plt.ylabel("Mean Salary")
plt.grid(axis="y", linestyle="--", alpha=0.6)

plt.show()

# boxplot for distribution by group
plt.figure(figsize=(8, 5))

sns.boxplot(
    x="city",
    y="salary",
    data=df,
    palette="Set2"
)

plt.title("Salary Distribution by City")
plt.show()

# 6. CORRELATION

corr = df.corr(numeric_only=True)
print("\nCorrelation matrix:\n", corr)

plt.figure(figsize=(8, 6))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    linewidths=0.5
)

plt.title("Correlation Heatmap")
plt.show()

# 7. OUTLIERS

plt.figure(figsize=(8, 5))

sns.boxplot(x=df["salary"], color="lightblue")

plt.title("Salary Outliers")
plt.show()

# simple filtering example
df_filtered = df[df["salary"] < df["salary"].quantile(0.99)]

# 8. UNIQUE VALUES (CATEGORICAL)

print("\nCity distribution:\n", df["city"].value_counts())

plt.figure(figsize=(8, 5))

df["city"].value_counts().plot(
    kind="bar",
    color="coral",
    edgecolor="black"
)

plt.title("City Distribution")
plt.xlabel("City")
plt.ylabel("Count")

plt.show()

# 9. FINAL QUICK SUMMARY

print("\nSummary:")
print("- Rows:", df.shape[0])
print("- Columns:", df.shape[1])
print("- Missing total:", df.isna().sum().sum())
print("- Duplicate rows:", df.duplicated().sum())
```
