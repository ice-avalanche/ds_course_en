# Lesson 2: Python Basics

## 1. Variables and data types

Python is dynamically typed – no need to declare types.

```python
x = 10          # int
y = 3.14        # float
name = "Alice"  # string
flag = True     # boolean
```

Check type:

```python
type(x)
type(name)
```

Type conversion:

```python
int("10")
float(5)
str(100)
```

## 2. Arithmetic operations

```python
a = 10
b = 3

a + b    # addition
a - b    # subtraction
a * b    # multiplication
a / b    # division
a // b   # integer division
a % b    # remainder
a ** b   # power
```

## 3. Strings

```python
text = "data science"

text.upper()
text.lower()
text.capitalize()
```

Indexing:

```python
text[0]
text[-1]
```

Slicing:

```python
text[0:4]
text[:4]
text[5:]
```

Replace:

```python
text.replace("data", "ml")
```

Split:

```python
text.split(" ")
```

f-strings:

```python
name = "Alice"
age = 25

f"{name} is {age} years old"
```

## 4. Lists

Ordered collection.

```python
nums = [1, 2, 3, 4]
```

Access:

```python
nums[0]
nums[-1]
```

Modify:

```python
nums[0] = 10
```

Add elements:

```python
nums.append(5)
nums.extend([6, 7])
```

Remove:

```python
nums.remove(3)
nums.pop()
```

Length:

```python
len(nums)
```

Sort:

```python
nums.sort()
```

Reverse:

```python
nums.reverse()
```

## 5. List comprehension

Compact way to create lists.

```python
[x for x in range(10)]
```

With condition:

```python
[x for x in range(10) if x % 2 == 0]
```

Transform:

```python
[x**2 for x in range(5)]
```

## 6. Dictionaries

Key-value structure.

```python
user = {
    "name": "Alice",
    "age": 25
}
```

Access:

```python
user["name"]
```

Safe access:

```python
user.get("age")
user.get("salary", 0)
```

Add/update:

```python
user["age"] = 26
user["city"] = "Paris"
```

Keys and values:

```python
user.keys()
user.values()
user.items()
```

## 7. Sets

Unordered collection of unique elements.

```python
s = {1, 2, 3}
```

Add/remove:

```python
s.add(4)
s.remove(2)
```

Operations:

```python
a = {1, 2, 3}
b = {3, 4, 5}

a & b   # intersection
a | b   # union
a - b   # difference
```

## 8. Conditional statements

```python
x = 10

if x > 5:
    print("big")
elif x == 5:
    print("equal")
else:
    print("small")
```

## 9. Loops

### for loop

```python
for i in range(5):
    print(i)
```

Loop over list:

```python
nums = [1, 2, 3]

for x in nums:
    print(x)
```

With index:

```python
for i, x in enumerate(nums):
    print(i, x)
```

### while loop

```python
i = 0

while i < 5:
    print(i)
    i += 1
```

## 10. Functions

```python
def add(a, b):
    return a + b
```

Call:

```python
add(2, 3)
```

Default arguments:

```python
def greet(name="user"):
    return f"Hello, {name}"
```

## 11. Lambda functions

Short anonymous functions.

```python
f = lambda x: x * 2

f(5)
```

Common usage:

```python
nums = [1, 2, 3]

list(map(lambda x: x**2, nums))
```

## 12. Working with files

Write:

```python
with open("file.txt", "w") as f:
    f.write("hello")
```

Read:

```python
with open("file.txt", "r") as f:
    text = f.read()
```

## 13. Useful built-in functions

```python
len([1, 2, 3])
sum([1, 2, 3])
min([1, 2, 3])
max([1, 2, 3])
sorted([3, 1, 2])
```

## 14. Working with ranges

```python
range(5)        # 0..4
range(1, 5)     # 1..4
range(0, 10, 2) # step
```

Convert to list:

```python
list(range(5))
```

## 15. Basic data processing example

```python
data = [10, 20, 30, 40]

# filter
filtered = [x for x in data if x > 20]

# transform
scaled = [x / 10 for x in filtered]

# aggregate
result = sum(scaled)

result
```
