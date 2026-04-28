# Task 6: Feature Engineering

## Task

You are given a dataset. Create new features based on existing columns using pandas and numpy.

## Input Data

```python id="fe_task_load"
import pandas as pd
import numpy as np

df = pd.read_csv("data.csv")
```

## 1. Simple feature

* Create salary in thousands

```python id="fe_task_1"
df["salary_k"] = df["________"] / ________   # use "salary" and divide by 1000
```

## 2. Arithmetic features

* Create income per age
* Create squared age

```python id="fe_task_2"
df["income_per_age"] = df["________"] / df["________"]   # salary / age

df["age_squared"] = df["________"] ** ________           # age ** 2
```

## 3. Conditional features

* Create binary feature high_salary

```python id="fe_task_3"
df["high_salary"] = df["________"] > ________   # salary > 60000 (example)
```

* Create categorical feature

```python id="fe_task_4"
df["category"] = np.________(
    df["salary"] > ________,   # threshold like 60000
    "high",
    "low"
)   # function: where
```

## 4. Multiple conditions

```python id="fe_task_5"
df["group"] = np.________(
    [
        df["salary"] > ________,   # first threshold (e.g. 70000)
        df["salary"] > ________    # second threshold (e.g. 50000)
    ],
    [
        "top",
        "mid"
    ],
    default="low"
)   # function: select
```

## 5. Text features

* Lowercase city
* Length of name

```python id="fe_task_6"
df["city_lower"] = df["________"].str.________()   # lower()

df["name_len"] = df["________"].str.________()     # len()
```

## 6. Date features

* Convert date
* Extract year and month

```python id="fe_task_7"
df["date"] = pd.to_datetime(df["________"])   # column with date

df["year"] = df["date"].dt.________   # year
df["month"] = df["date"].dt.________  # month
```

## 7. Time difference

```python id="fe_task_8"
df["days_since"] = (
    pd.Timestamp("today") - df["________"]
).dt.________   # days
```

## 8. Binning

* Create age groups

```python id="fe_task_9"
df["age_group"] = pd.________(
    df["age"],
    bins=[0, 25, 40, 100],
    labels=["young", "adult", "senior"]
)   # function: cut
```

## 9. Encoding

* Label encoding

```python id="fe_task_10"
df["city_code"] = df["city"].astype("________").cat.________   # "category", codes
```

* One-hot encoding

```python id="fe_task_11"
df = pd.________(df, columns=["________"])   # get_dummies, column "city"
```

## 10. Scaling

```python id="fe_task_12"
df["salary_scaled"] = (
    df["salary"] - df["salary"].________()   # mean
) / df["salary"].________()                 # std
```

## 11. Log transformation

```python id="fe_task_13"
df["salary_log"] = np.________(df["salary"])   # log1p
```

## 12. Aggregation-based feature

```python id="fe_task_14"
mean_salary = df.groupby("________")["________"].________()   # city, salary, mean

df["city_avg_salary"] = df["________"].map(mean_salary)       # map by city
```

## 13. Rank feature

```python id="fe_task_15"
df["salary_rank"] = df["salary"].________(ascending=________)   # rank, False for descending
```

## 14. Rolling feature

```python id="fe_task_16"
df = df.________("date")   # sort_values

df["rolling_mean"] = df["salary"].________(3).________()   # rolling, mean
```

## 15. Interaction feature

```python id="fe_task_17"
df["age_salary"] = df["________"] * df["________"]   # age * salary
```

## 16. Feature selection

```python id="fe_task_18"
df.________(numeric_only=True)   # correlation matrix (corr)
```

* Drop column

```python id="fe_task_19"
df = df.________(columns=["________"])   # drop, e.g. "id"
```

## 17. Pipeline-style

```python id="fe_task_20"
df = (
    df
    .________(   # assign
        salary_k=df["salary"] / 1000,
        high_salary=df["salary"] > 60000
    )
)
```
