# Lesson 6: Feature Engineering

## 1. Setup

```python id="fe_setup"
import pandas as pd
import numpy as np
```

Load data:

```python id="fe_load"
df = pd.read_csv("data.csv")
```

## 2. What is feature engineering

Feature engineering – creating new variables from existing data to improve analysis or models.

Typical goals:

* make patterns more visible
* convert data to usable format
* add domain logic

## 3. Simple feature creation

```python id="fe_simple"
df["salary_k"] = df["salary"] / 1000
```

## 4. Arithmetic features

```python id="fe_arith"
df["income_per_age"] = df["salary"] / df["age"]
df["age_squared"] = df["age"] ** 2
```

## 5. Conditional features

```python id="fe_cond"
df["high_salary"] = df["salary"] > 60000
```

More complex:

```python id="fe_cond2"
df["category"] = np.where(df["salary"] > 60000, "high", "low")
```

Multiple conditions:

```python id="fe_cond3"
df["group"] = np.select(
    [
        df["salary"] > 70000,
        df["salary"] > 50000
    ],
    [
        "top",
        "mid"
    ],
    default="low"
)
```

## 6. Working with text

```python id="fe_text"
df["city_lower"] = df["city"].str.lower()
```

Length:

```python id="fe_text_len"
df["name_len"] = df["name"].str.len()
```

Split:

```python id="fe_text_split"
df["domain"] = df["email"].str.split("@").str[1]
```

## 7. Working with dates

Convert:

```python id="fe_date_convert"
df["date"] = pd.to_datetime(df["date"])
```

Extract components:

```python id="fe_date_parts"
df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["day"] = df["date"].dt.day
df["weekday"] = df["date"].dt.weekday
```

Time difference:

```python id="fe_date_diff"
df["days_since"] = (pd.Timestamp("today") - df["date"]).dt.days
```

## 8. Binning (discretization)

```python id="fe_bin"
df["age_group"] = pd.cut(
    df["age"],
    bins=[0, 25, 40, 100],
    labels=["young", "adult", "senior"]
)
```

## 9. Encoding categories

### Label encoding

```python id="fe_label"
df["city_code"] = df["city"].astype("category").cat.codes
```

### One-hot encoding

```python id="fe_ohe"
df = pd.get_dummies(df, columns=["city"])
```

## 10. Scaling features

```python id="fe_scale"
df["salary_scaled"] = (df["salary"] - df["salary"].mean()) / df["salary"].std()
```

## 11. Log transformation

```python id="fe_log"
df["salary_log"] = np.log1p(df["salary"])
```

Used for skewed data.

## 12. Aggregation-based features

```python id="fe_group"
mean_salary = df.groupby("city")["salary"].mean()

df["city_avg_salary"] = df["city"].map(mean_salary)
```

## 13. Rank features

```python id="fe_rank"
df["salary_rank"] = df["salary"].rank(ascending=False)
```

## 14. Rolling features (time-based)

```python id="fe_roll"
df = df.sort_values("date")

df["rolling_mean"] = df["salary"].rolling(3).mean()
```

## 15. Interaction features

```python id="fe_interact"
df["age_salary"] = df["age"] * df["salary"]
```

## 16. Feature selection (basic)

```python id="fe_select"
df.corr(numeric_only=True)
```

Remove useless columns:

```python id="fe_drop"
df = df.drop(columns=["id"])
```

## 17. Pipeline-style transformation

```python id="fe_pipeline"
df = (
    df
    .assign(
        salary_k=df["salary"] / 1000,
        high_salary=df["salary"] > 60000
    )
)
```

## 18. Real example

```python id="fe_real"
df = pd.read_csv("data.csv")

df["date"] = pd.to_datetime(df["date"])

df = (
    df
    .assign(
        salary_k=df["salary"] / 1000,
        high_salary=df["salary"] > 60000,
        year=df["date"].dt.year,
        month=df["date"].dt.month
    )
)

city_mean = df.groupby("city")["salary"].mean()

df["city_avg_salary"] = df["city"].map(city_mean)

df.head()
```
