---
dg-publish: true
---
---
# 🐍 Python Cheat Sheet: From Basics to Advanced with Detailed Explanations, Logic, and Syntax Meaning

---

## 🔰 Getting Started with Python

### Hello World

```python
print("Hello, World!")
```

**Purpose**: Display output to the console.  
**Logic**: This line of code outputs the string "Hello, World!" to the screen.  
**Syntax**: `print()` is a built-in function; double quotes are used for string literals.

### Comments

```python
# This is a comment
```

**Purpose**: Explain code, ignored by Python interpreter.  
**Logic**: Useful for documentation or disabling code.  
**Syntax**: Starts with `#` — everything after is ignored by the interpreter.

### Variables

```python
name = "Crus"
age = 22
```

**Purpose**: Store values for reuse.  
**Logic**: Assign a value using the `=` operator. Python detects type automatically.  
**Syntax**: Variable name = value.

### Data Types

```python
x = 5           # int (whole number)
y = 3.14        # float (decimal number)
z = "Hello"     # str (text)
is_valid = True # bool (boolean: True/False)
```

**Purpose**: Represent different types of data.  
**Logic**: Python automatically infers the type during assignment.  
**Syntax**: Assign literal values directly.

---

## 🧮 Operators

```python
# Arithmetic: + - * / % ** //
# Comparison: == != > < >= <=
# Logical: and or not
# Assignment: = += -= *=
```

**Purpose**: Perform math, comparisons, and logic operations.  
**Logic**: Used to manipulate and compare values.  
**Syntax**: Infix notation (between operands).

---

## 🔁 Conditionals

```python
if x > 10:
    print("Greater than 10")
elif x == 10:
    print("Equal to 10")
else:
    print("Less than 10")
```

**Purpose**: Make decisions based on conditions.  
**Logic**: Checks each condition in order. Runs the first true block.  
**Syntax**: `if`, `elif`, `else` followed by indented block.

---

## 🔄 Loops

### For Loop

```python
for i in range(5):
    print(i)
```

**Purpose**: Repeat a block of code a set number of times.  
**Logic**: `range(5)` produces 0–4. `i` takes each value.  
**Syntax**: `for` variable `in` iterable `:`

### While Loop

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

**Purpose**: Repeat while condition is true.  
**Logic**: `i` increases by 1 each loop. Stops when `i >= 5`.  
**Syntax**: `while` condition `:` followed by indented block.

### Loop Control

```python
for i in range(5):
    if i == 3:
        break
    if i == 1:
        continue
    print(i)
```

**Purpose**:

- `break`: exit loop early.
    
- `continue`: skip rest of current loop.  
    **Logic**: Controls how loop behaves inside its body.
    

---

## 🧠 Functions

```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Crus"))
```

**Purpose**: Reuse logic by encapsulating it in named blocks.  
**Logic**: `name` is a parameter. `return` sends output back.  
**Syntax**: `def` defines function. `f"..."` formats the string.

---

## 🧱 Data Structures

### Lists

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")
print(fruits[0])
```

**Purpose**: Store ordered, mutable collection of items.  
**Syntax**: Brackets `[]`; use `.append()` to add items.

### Tuples

```python
coordinates = (10, 20)
```

**Purpose**: Like lists, but immutable (unchangeable).  
**Syntax**: Parentheses `()` used for fixed data.

### Sets

```python
unique_numbers = {1, 2, 3}
unique_numbers.add(4)
```

**Purpose**: Unordered collection of unique items.  
**Logic**: Automatically removes duplicates.  
**Syntax**: Curly braces `{}` for set literals.

### Dictionaries

```python
person = {"name": "Crus", "age": 22}
print(person["name"])
```

**Purpose**: Key-value pairs.  
**Logic**: Each value is accessed via a unique key.  
**Syntax**: Curly braces with `key: value` pairs.

---

## 🧰 Built-in Functions

```python
len(), range(), type(), sum(), max(), min(), sorted(), list(), dict()
```

**Purpose**: Built-in tools to perform common tasks.  
**Logic**: Work across data types. Save time.

---

## 🧪 List Comprehensions

```python
evens = [x for x in range(10) if x % 2 == 0]
```

**Purpose**: Short way to create lists.  
**Logic**: Loop inside brackets with optional condition.

---

## ⚡ Lambda Functions

```python
double = lambda x: x * 2
print(double(4))
```

**Purpose**: Anonymous function. Used for simple, one-line functions.  
**Syntax**: `lambda` followed by parameters and expression.

---

## 🛠 Error Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("You can't divide by zero!")
finally:
    print("Execution complete")
```

**Purpose**: Prevent crashes by handling errors.  
**Logic**: `try` runs code; `except` catches specific errors; `finally` always runs.

---

## 📁 File Handling

```python
# Write
with open("data.txt", "w") as file:
    file.write("Hello, World!")

# Read
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
```

**Purpose**: Read and write to files.  
**Syntax**: `with` ensures the file closes automatically. Modes: `"r"` = read, `"w"` = write.

---

## 🧩 Decorators

```python
def decorator_func(original_func):
    def wrapper():
        print("Before the function runs")
        return original_func()
    return wrapper

@decorator_func
def say_hello():
    print("Hello!")

say_hello()
```

**Purpose**: Add extra behavior to functions.  
**Logic**: `@decorator` syntax wraps the function with another.

---

## 🔁 Generators

```python
def counter():
    i = 0
    while True:
        yield i
        i += 1
```

**Purpose**: Generate values one at a time (lazy evaluation).  
**Syntax**: `yield` pauses function and resumes later.

---

## 📄 File Parsing (CSV/JSON)

```python
# CSV
import csv
with open("data.csv") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# JSON
import json
with open("data.json", "r") as f:
    data = json.load(f)
    print(data)
```

**Purpose**: Load and work with structured data.  
**CSV**: Plain text with commas.  
**JSON**: Hierarchical, readable format.

---

## 📦 Modules & Packages

```python
# math_utils.py
def square(x): return x * x

# main.py
import math_utils
print(math_utils.square(4))
```

**Purpose**: Organize code in files and folders.  
**Logic**: `import` keyword loads code from other files.

---

## 🧱 Object-Oriented Programming

```python
class Person:
    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Hi, I'm {self.name}"

p = Person("Crus")
print(p.greet())
```

**Purpose**: Represent real-world objects with properties and methods.  
**Syntax**: `class`, `__init__()` constructor, `self` refers to instance.

---

## 📊 NumPy & Pandas

```python
import numpy as np
import pandas as pd

arr = np.array([1, 2, 3])
df = pd.DataFrame({"A": [1, 2], "B": [3, 4]})
```

**Purpose**:

- **NumPy**: Efficient numerical computations.
    
- **Pandas**: Tabular data analysis (like Excel).
    

---

## 📅 DateTime

```python
from datetime import datetime
now = datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S"))
```

**Purpose**: Work with dates and times.  
**Syntax**: `strftime()` formats the output.

---

## 💡 Tips

- Use clear variable names
    
- Keep code DRY (Don't Repeat Yourself)
    
- Use virtual environments for projects
    
- Use `help(function)` for quick docs in interpreter
    

---

✅ This cheat sheet now includes logic + syntax explanation for:

- Basics to Advanced Python
    
- OOP, Decorators, File Handling
    
- NumPy, Pandas, CSV/JSON, Errors, Dates
    

Perfect for learning or refreshing any concept!