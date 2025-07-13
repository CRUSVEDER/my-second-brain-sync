---
dg-publish:
---
---
## 🧠 Functions (Expanded, Custom, and Beginner-Friendly Explanation)

### Function with Default Parameter

```python
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet("Crus")  # Calling the function with custom input
greet()         # Calling the function without input, uses default
```

**Purpose**: Function greets a person. If no name is given, it uses "Guest".  
**Logic**:

- If a name is passed, use it
    
- If not, use the default: `Guest`  
    **Syntax**: `def function_name(param=value):`  
    **How to Recall/Use**:
    
- Call it later in code with: `greet("your_name")` or just `greet()`
    

```
Main Program
   |
   |---> greet("Crus")
              |
              |---> Function executes: print("Hello, Crus!")
              |
              |---> Returns control back to main
```

### Function with Multiple Parameters and Return

```python
def add(a, b):
    return a + b

result = add(10, 5)  # Call and store result
print("Sum:", result)
```

**Purpose**: Add two numbers and return the result.  
**Logic**:

- `a` and `b` are parameters
    
- `return` sends the result back  
    **Syntax**: Use `return` to send a value back to the caller  
    **How to Recall/Use**:
    
- Store the result in a variable: `result = add(3, 4)`
    
- Use directly in expressions: `total = add(price, tax)`
    
```
Main Program
   |
   |---> result = add(10, 5)
                   |
                   |---> Function executes: return 10 + 5 → 15
                   |---> 'result' gets value 15
```
### Function with Arbitrary Arguments

```python
def multiply_all(*args):
    result = 1
    for num in args:
        result *= num
    return result

print(multiply_all(2, 3, 4))  # Output: 24
```

**Purpose**: Multiply any number of inputs.  
**Logic**:

- `*args` collects values into a tuple
    
- Loop through each value and multiply them  
    **Syntax**: `*args` lets function take unlimited arguments  
    **How to Recall/Use**:
    
- Can call with any number of arguments: `multiply_all(1, 2, 3, 4)`
    

### Function with Keyword Arguments

```python
def show_profile(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

show_profile(name="Crus", age=22)
```

**Purpose**: Accepts named parameters (like a form).  
**Logic**:

- `**kwargs` collects keyword arguments into a dictionary
    
- `.items()` gets key-value pairs to print  
    **Syntax**: `**kwargs` handles flexible named inputs  
    **How to Recall/Use**:
    
- Use named arguments like: `show_profile(role="Admin", location="India")`
    

### Recursive Function Example

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n-1)

print(factorial(5))  # Output: 120
```

**Purpose**: Calculates factorial using recursion.  
**Logic**:

- `factorial(n)` calls itself with smaller `n`
    
- Base case: when `n` is 0, return 1  
    **Syntax**:
    
- Recursive functions must have a stop condition (base case)  
    **How to Recall/Use**:
    
- Simply call with a number: `factorial(5)` or `factorial(user_input)`
    
- Use to solve problems like factorial, Fibonacci, etc.
    
```
Calling factorial(3)
   |
   |---> factorial(3)
           |---> 3 * factorial(2)
                       |---> 2 * factorial(1)
                                   |---> 1 * factorial(0)
                                               |---> return 1 (base case)
                                   |<--- return 1 * 1 = 1
                       |<--- return 2 * 1 = 2
           |<--- return 3 * 2 = 6
```
### 🔍 Real-Life Function Examples Used in Industry

#### 1. Email Validator

```python
import re

def is_valid_email(email):
    pattern = r"^[\w\.-]+@[\w\.-]+\.\w+$"
    return re.match(pattern, email) is not None

print(is_valid_email("user@example.com"))  # True
```

**Use Case**: Web development, form validation. Ensures a user enters a proper email format.

#### 2. Logging Function

```python
from datetime import datetime

def log_event(message):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    print(f"[{timestamp}] {message}")

log_event("User logged in")
```

**Use Case**: Used in backend servers, apps, and automation tools to keep track of system activity.

#### 3. Data Cleaning Function

```python
def clean_text(text):
    return text.strip().lower().replace("\n", " ")

print(clean_text("  Hello\nWorld  "))  # 'hello world'
```

**Use Case**: Data preprocessing in machine learning or analytics pipelines.

#### 4. Pagination Function

```python
def paginate(data, page_size):
    for i in range(0, len(data), page_size):
        yield data[i:i+page_size]

items = list(range(1, 21))
for page in paginate(items, 5):
    print(page)
```

**Use Case**: Common in APIs, blogs, and product listings to split large results into pages.

#### 5. Retry Mechanism

```python
import time

def retry(func, retries=3):
    for i in range(retries):
        try:
            return func()
        except Exception as e:
            print(f"Attempt {i+1} failed: {e}")
            time.sleep(1)

# Example usage
def flaky_function():
    raise ValueError("Failed task")

retry(flaky_function)
```

**Use Case**: Networking, web scraping, or microservices where some failures are expected.

---
## 🧭 Function Flow Diagrams (Visual Logic)



### Recursive Function Flow (factorial)

```
Calling factorial(3)
   |
   |---> factorial(3)
           |---> 3 * factorial(2)
                       |---> 2 * factorial(1)
                                   |---> 1 * factorial(0)
                                               |---> return 1 (base case)
                                   |<--- return 1 * 1 = 1
                       |<--- return 2 * 1 = 2
           |<--- return 3 * 2 = 6
```

### Real Life Example Flow (Email Validator)

```
Main Program
   |
   |---> is_valid_email("user@example.com")
                |
                |---> Checks pattern using regex
                |---> Matches, returns True
   |---> Output: True (valid email)
```

### Retry Logic Flow

```
Main Program
   |
   |---> retry(flaky_function, retries=3)
                |
                |---> Attempt 1: fails → print error
                |---> Wait 1 sec
                |---> Attempt 2: fails → print error
                |---> Wait 1 sec
                |---> Attempt 3: fails → print error
                |---> Ends, returns None
```

---

(remaining content unchanged)