# Task 1: Basics of Python and pandas

## Task

You are given a small dataset with product sales. Complete the steps below using pandas.

## Input Data

```python
import pandas as pd

data = {
    "product": ["A", "B", "C", "D"],
    "sales": [120, 80, 200, 150],
    "price": [10, 20, 15, 25]
}
```

## 1. Create DataFrame

* Create a DataFrame from the dictionary
* Display it

```python
df = pd.________(data)  # function to create DataFrame

print(df.________())    # method to display first rows
```

## 2. Create a new feature

* Add a new column `revenue`
* Use formula: sales * price

```python
df["revenue"] = df["sales"] * df["________"]  # multiply by which column?

df.head()
```

## 3. Basic metrics

Calculate:

* total sales
* average sales
* maximum revenue

```python
total_sales = df["sales"].________()     # sum of column

average_sales = df["sales"].________()   # mean of column

max_revenue = df["revenue"].________()   # max value
```

## 4. Find specific rows

Find:

* product with the highest sales
* product with the lowest price

```python
# highest sales
df[df["sales"] == df["sales"].________()]   # function to get max

# lowest price
df[df["price"] == df["price"].________()]  # function to get min
```

## 5. Analysis

* Find the product with the highest revenue

```python
df[df["revenue"] == df["revenue"].________()]
```

* Extract only the product name

```python
df.loc[
    df["revenue"] == df["revenue"].max(),  # condition
    ["________"]                           # column name with product
]
```
