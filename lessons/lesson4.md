# Lesson 4: Data Visualization

## 1. Setup

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

Optional:

```python
import seaborn as sns
```

## 2. Simple plot (pandas)

```python
df = pd.DataFrame({
    "x": [1, 2, 3, 4],
    "y": [10, 20, 15, 30]
})

df["y"].plot()
plt.show()
```

## 3. Line plot

```python
plt.plot(df["x"], df["y"])
plt.show()
```

Add labels:

```python
plt.plot(df["x"], df["y"])
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Line plot")
plt.show()
```

## 4. Multiple lines

```python
df = pd.DataFrame({
    "x": [1, 2, 3, 4],
    "y1": [10, 20, 15, 30],
    "y2": [5, 15, 10, 25]
})

plt.plot(df["x"], df["y1"])
plt.plot(df["x"], df["y2"])
plt.show()
```

## 5. Scatter plot

```python
plt.scatter(df["x"], df["y1"])
plt.show()
```

Useful for relationships.

## 6. Histogram

```python
data = np.random.randn(1000)

plt.hist(data, bins=30)
plt.show()
```

## 7. Bar chart

```python
df = pd.DataFrame({
    "city": ["NY", "LA", "SF"],
    "sales": [100, 150, 120]
})

plt.bar(df["city"], df["sales"])
plt.show()
```

## 8. Boxplot

```python
data = np.random.randn(100)

plt.boxplot(data)
plt.show()
```

Shows distribution, outliers.

## 9. Seaborn basics

### Histogram

```python
sns.histplot(data)
plt.show()
```

### Scatter with regression

```python
sns.regplot(x=df["x"], y=df["y1"])
plt.show()
```

### Boxplot

```python
sns.boxplot(x=df["city"], y=df["sales"])
plt.show()
```

## 10. Working with categories

```python
df = pd.DataFrame({
    "city": ["NY", "NY", "LA", "SF", "SF"],
    "sales": [100, 120, 150, 130, 140]
})

df.groupby("city")["sales"].mean().plot(kind="bar")
plt.show()
```

## 11. Subplots

```python
fig, ax = plt.subplots(1, 2)

ax[0].plot(df["sales"])
ax[1].hist(df["sales"])

plt.show()
```

## 12. Figure size

```python
plt.figure(figsize=(8, 4))
plt.plot(df["sales"])
plt.show()
```

## 13. Grid and style

```python
plt.plot(df["sales"])
plt.grid(True)
plt.show()
```

## 14. Saving plot

```python
plt.plot(df["sales"])
plt.savefig("plot.png")
```

## 15. Real example

```python
import pandas as pd
import matplotlib.pyplot as plt

# load data
df = pd.read_csv("data.csv")

plt.figure(figsize=(8, 5))  # figure size

plt.scatter(
    df["age"], 
    df["salary"],
    color="steelblue",        # point color
    s=80,                     # point size
    alpha=0.7,                # transparency
    edgecolors="black",       # border color
    linewidth=1.2,            # border width
    marker="o",               # marker type
    label="Data points"       # legend label
)

# title and labels
plt.title("Age vs Salary", fontsize=14, fontweight="bold")
plt.xlabel("Age", fontsize=12)
plt.ylabel("Salary", fontsize=12)

# axis limits
plt.xlim(0, df["age"].max() + 5)
plt.ylim(0, df["salary"].max() * 1.1)

# grid
plt.grid(True, linestyle="--", alpha=0.6)

# legend
plt.legend()

# annotation (example point)
plt.annotate(
    "Example",
    xy=(df["age"].iloc[0], df["salary"].iloc[0]),
    xytext=(df["age"].iloc[0] + 2, df["salary"].iloc[0] + 5000),
    arrowprops=dict(facecolor="black", arrowstyle="->"),
    fontsize=10
)

# show plot
plt.show()
```

## 16. When to use what

* Line plot – trends over time
* Scatter – relationships
* Histogram – distribution
* Bar – categories
* Boxplot – outliers
