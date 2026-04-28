# Lesson 1: Google Colab + Environment

## 1. Google Colab: quick start

Google Colab is a cloud environment for running Python code. No local setup is required.

How to start:

1. Open: [https://colab.research.google.com](https://colab.research.google.com)
2. Click “New Notebook”
3. Rename the file

## 2. Interface

A notebook consists of two types of cells:

* Code – runs Python
* Text – Markdown

Create a cell:

* Code
* Text

Run a cell:

* Shift + Enter (run and move next)
* Ctrl + Enter (run and stay in current cell)

Example:

```python
print("Hello, Colab")
```

## 3. Basic operations

Multiple statements:

```python
x = 10
y = 5

x + y
```

The last line output is displayed automatically.

## 4. Working with files

### Check files in environment

```python
import os

os.listdir()
```

Lists files in the current directory.

### Upload file from local machine

```python
from google.colab import files

uploaded = files.upload()
```

The uploaded file becomes available in the session.

### Read CSV

```python
import pandas as pd

df = pd.read_csv("data.csv")
df.head()
```

## 5. Google Drive integration

### Mount Drive

```python
from google.colab import drive
drive.mount('/content/drive')
```

### Read file from Drive

```python
df = pd.read_csv("/content/drive/MyDrive/data/data.csv")
```

## 6. Installing libraries

Install:

```python
!pip install pandas numpy matplotlib
```

Import:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

## 7. Environment check

Python version:

```python
import sys
print(sys.version)
```

Installed packages:

```python
!pip list
```
