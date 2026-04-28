# Lesson 3: pandas Basics + Filtering

## 1. Import and setup

```python
import pandas as pd
import numpy as np
```

## 2. Creating DataFrame

From dictionary:

```python
data = {
    "age": [25, 30, 22, 40],
    "salary": [50000, 60000, 45000, 80000],
    "city": ["NY", "LA", "NY", "SF"]
}

df = pd.DataFrame(data)
df
```

From CSV:

```python
df = pd.read_csv("data.csv")
```

## 3. Basic inspection

```python
df.head()       # first rows
df.tail()       # last rows
df.shape        # (rows, columns)
df.columns      # column names
df.dtypes       # data types
```

## 4. Data info

```python
df.info()
```

## 5. Summary statistics

```python
df.describe()
```

Include all columns:

```python
df.describe(include="all")
```

## 6. Selecting data

### Single column

```python
df["age"]
```

### Multiple columns

```python
df[["age", "salary"]]
```

### Row selection with loc

```python
df.loc[0]
```

```python
df.loc[0:2]
```

### Row selection with iloc

```python
df.iloc[0]
df.iloc[0:2]
```

## 7. Filtering rows

### Basic condition

```python
df[df["age"] > 25]
```

### Multiple conditions

```python
df[(df["age"] > 25) & (df["salary"] > 50000)]
```

```python
df[(df["city"] == "NY") | (df["city"] == "SF")]
```

### isin

```python
df[df["city"].isin(["NY", "SF"])]
```

### not condition

```python
df[~(df["age"] > 30)]
```

## 8. Column operations

### Create new column

```python
df["salary_k"] = df["salary"] / 1000
```

### Conditional column

```python
df["high_salary"] = df["salary"] > 60000
```

### Apply function

```python
df["age_plus_10"] = df["age"].apply(lambda x: x + 10)
```

## 9. Sorting

```python
df.sort_values("salary")
```

Descending:

```python
df.sort_values("salary", ascending=False)
```

Multiple columns:

```python
df.sort_values(["city", "salary"])
```

## 10. Unique values

```python
df["city"].unique()
```

```python
df["city"].nunique()
```

## 11. Value counts

```python
df["city"].value_counts()
```

## 12. Handling missing values

Check missing:

```python
df.isna()
```

Count missing:

```python
df.isna().sum()
```

Drop rows:

```python
df.dropna()
```

Fill values:

```python
df.fillna(0)
```

## 13. Basic aggregation

```python
df["salary"].mean()
df["salary"].sum()
df["salary"].min()
df["salary"].max()
```

## 14. Groupby (basic)

```python
df.groupby("city")["salary"].mean()
```

Multiple aggregations:

```python
df.groupby("city")["salary"].agg(["mean", "max", "count"])
```

## 15. Renaming columns

```python
df.rename(columns={"salary": "income"})
```

## 16. Dropping columns

```python
df.drop(columns=["city"])
```

## 17. Reset index

```python
df.reset_index()
```

## 18. Chaining operations

```python
result = (
    df[df["age"] > 25]
    .sort_values("salary", ascending=False)
    [["age", "salary"]]
)
```

## 19. Real example

```python
df = pd.read_csv("data.csv")

result = (
    df[df["salary"] > 50000]
    .assign(salary_k=df["salary"] / 1000)
    .sort_values("salary_k", ascending=False)
)

result.head()
```
