# Task 2: Filtering and Basic Metrics

## Task

You are given a dataset with customer information. Complete the steps below using pandas.

## Input Data

```python
import pandas as pd

data = {
    "customer_id": [1, 2, 3, 4, 5, 6, 7],
    "age": [25, 40, 35, 28, 50, 23, 45],
    "country": ["US", "UK", "US", "DE", "DE", "US", "UK"],
    "purchase_amount": [100, 250, 80, 300, 150, 60, 500],
    "category": ["A", "B", "A", "C", "B", "A", "C"]
}
```

## 1. Create DataFrame

* Create a DataFrame from the dictionary
* Display it

```python
df = pd.________(data)   # function to create DataFrame

print(df.________())     # display first rows
```

## 2. Filter customers from the US

* Select only rows where country is "US"

```python
us_customers = df[ df["________"] == "US" ]   # column with country

us_customers
```

## 3. Average purchase amount (US customers)

* Calculate average purchase amount for US customers

```python
avg_purchase_us = us_customers["________"].________()   # column + mean

avg_purchase_us
```

## 4. Total revenue for customers older than 30

* Filter customers with age > 30
* Calculate total purchase amount

```python
older_customers = df[ df["________"] > 30 ]   # age column

total_revenue = older_customers["________"].________()   # sum

total_revenue
```
