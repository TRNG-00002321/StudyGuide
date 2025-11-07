# Python Study Guide

## Full Stack Overview

Full stack development refers to the practice of working on both the front-end and back-end parts of a web application. A full stack developer is proficient in multiple layers of the technology stack, including the user interface, server-side logic, databases, and often deployment and DevOps.

In the context of Python, full stack development typically involves:

### Front-End

The front-end is the part of the application that users interact with directly. It is usually built using **HTML**, **CSS**, and **JavaScript**. While Python is not used directly in the browser, Python developers often use frameworks like **Django** or **Flask** in combination with front-end technologies. Tools like **React** or **Vue.js** are commonly integrated for dynamic interfaces.

### Back-End

The back-end handles business logic, database interactions, and server-side processing. Python frameworks like **Django** and **Flask** are popular for building robust back-end systems.

### Database

Databases store and manage application data. Python developers often use relational databases like **PostgreSQL** or **MySQL**, or NoSQL databases like **MongoDB**. ORMs (Object-Relational Mappers) like **Django ORM** or **SQLAlchemy** simplify database interactions.

### Deployment

Deployment involves making the application accessible on the internet. Python applications are commonly deployed using platforms like **Heroku**, **AWS**, or **Docker** containers. Web servers like **Gunicorn** or **uWSGI** are used in production environments.

## Interpreter vs Compiler

Programming languages are typically executed using either an **interpreter** or a **compiler**, each with distinct characteristics in how they process code.

### Interpreter

An interpreter reads and executes code line-by-line at runtime. It does not produce a separate machine code file; instead, it directly runs the source code. Python is an interpreted language.

**Characteristics:**
- Executes code line-by-line
- Easier to debug due to immediate feedback
- Slower execution compared to compiled languages
- No separate executable is created

**Example:**
When running a Python script:
```bash
python my_script.py
```
The Python interpreter reads and executes the code in `my_script.py` line-by-line.

### Compiler

A compiler translates the entire source code into machine code (binary) before execution. This compiled code is stored in an executable file that can be run independently of the source code.

**Characteristics:**
- Translates entire code before execution
- Faster execution after compilation
- Errors are reported after the entire code is analyzed
- Produces a standalone executable

**Example:**
A C program is compiled using:
```bash
gcc program.c -o program
```
This creates an executable `program` that can be run without the source code.

### Summary

| Feature         | Interpreter                | Compiler                     |
|----------------|----------------------------|------------------------------|
| Execution       | Line-by-line               | Entire program at once       |
| Speed           | Slower                     | Faster after compilation     |
| Output          | No separate file           | Executable file              |
| Error Handling  | Stops at first error       | Reports all errors together  |
| Example         | Python                     | C, C++, Java (compiled to bytecode) |

## REPL and Jupyter

### REPL (Read-Eval-Print Loop)

REPL is an interactive programming environment that takes single user inputs (reads), evaluates them, and returns the result to the user (prints), then loops back for more input. Python’s REPL is accessible by simply running `python` or `python3` in a terminal.

**Characteristics:**
- Great for testing small code snippets
- Immediate feedback for learning and debugging
- No need to write and save a full script

**Example:**
```bash
$ python
>>> 2 + 2
4
>>> print("Hello")
Hello
```

REPL is especially useful for experimenting with Python syntax, functions, and libraries in real time.

### Jupyter Notebooks

Jupyter Notebooks provide a web-based interactive environment for writing and running code in chunks called "cells." They are widely used in data science, machine learning, and education due to their ability to mix code, output, and rich text (Markdown) in a single document.

**Key Features:**
- Supports code, visualizations, and narrative text
- Allows step-by-step execution of code cells
- Ideal for data analysis, visualization, and documentation

**Example:**
A Jupyter cell might contain:
```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [4, 5, 6])
plt.title("Simple Plot")
plt.show()
```

**Markdown cells** can be used to explain the code:
```markdown
### This plot shows a simple line chart using Matplotlib.
```

Jupyter Notebooks can be run locally using `jupyter notebook` or in cloud environments like Google Colab or JupyterHub.

### Summary

| Feature         | REPL                          | Jupyter Notebook                     |
|----------------|-------------------------------|--------------------------------------|
| Interface       | Command-line                  | Web-based                            |
| Use Case        | Quick testing, debugging      | Data analysis, teaching, documentation |
| Output Style    | Inline in terminal            | Inline below each cell               |
| Supports Markdown | No                          | Yes                                  |

## What is Python?

Python is a high-level, interpreted programming language known for its simplicity, readability, and versatility. It was created by **Guido van Rossum** and first released in **1991**. Python emphasizes code readability and allows developers to express concepts in fewer lines of code compared to many other languages.

### Key Features

- **Easy to Learn and Use**: Python has a clean and straightforward syntax, making it ideal for beginners.
- **Interpreted Language**: Python code is executed line-by-line, which makes debugging easier.
- **Dynamically Typed**: Variables do not need explicit declaration of their type.
- **High-Level Language**: Abstracts many low-level details like memory management.
- **Extensive Standard Library**: Comes with a wide range of modules and packages for various tasks.
- **Cross-Platform**: Python runs on Windows, macOS, Linux, and more.

### Common Use Cases

- **Web Development**: Using frameworks like Django and Flask.
- **Data Science and Machine Learning**: With libraries like NumPy, pandas, scikit-learn, and TensorFlow.
- **Automation and Scripting**: Automating repetitive tasks and writing scripts for system operations.
- **Software Development**: Building desktop and command-line applications.
- **Education**: Widely used as a first programming language in schools and universities.

### Example

A simple Python program to print a greeting:

```python
def greet(name):
    print(f"Hello, {name}!")

greet("World")
```

### Python 2 vs Python 3

Python 3 is the current and actively maintained version of the language. Python 2 reached end-of-life in 2020 and is no longer supported. Python 3 introduced several improvements and changes in syntax and behavior.

## Python Syntax

Python syntax refers to the set of rules that define how Python code is written and interpreted. It emphasizes readability and simplicity, using indentation and minimal punctuation to structure code.

### Indentation

Unlike many other languages that use braces `{}` to define code blocks, Python uses **indentation**. Consistent indentation is required and typically uses 4 spaces per level.

**Example:**
```python
if True:
    print("This is indented correctly")
```

Incorrect indentation will result in an `IndentationError`.

### Case Sensitivity

Python is **case-sensitive**, meaning `Variable`, `variable`, and `VARIABLE` are all treated as different identifiers.

### Statements and Line Breaks

Each line in Python is typically a separate statement. You can use a backslash `\` to continue a statement on the next line.

**Example:**
```python
total = 1 + 2 + 3 + \
        4 + 5
```

### Colons

Colons `:` are used to start code blocks, such as after `if`, `for`, `while`, `def`, and `class` statements.

**Example:**
```python
def greet():
    print("Hello")
```

### Comments

Comments begin with a `#` and are ignored by the interpreter. They are used to explain code and improve readability. (More on this in the **comments** section.)

**Example:**
```python
# This is a comment
print("Hello")  # This is an inline comment
```

### Semicolons

Semicolons are **optional** in Python. You can use them to separate multiple statements on a single line, but this is discouraged for readability.

**Example:**
```python
x = 5; y = 10
```

### Whitespace

Whitespace is significant in Python. Proper spacing around operators and after commas improves readability, though it is not strictly enforced by the interpreter.

## Comments

Comments in Python are used to explain code, make it more readable, and help others (or your future self) understand the purpose and logic behind it. Comments are ignored by the Python interpreter and do not affect program execution.

### Single-Line Comments

Single-line comments begin with the hash symbol `#`. Everything after the `#` on that line is treated as a comment.

**Example:**
```python
# This is a single-line comment
print("Hello")  # This is an inline comment
```

### Multi-Line Comments

Python does not have a specific syntax for multi-line comments like some other languages. However, you can use multiple single-line comments or a multi-line string (triple quotes) that is not assigned to a variable.

**Example using multiple single-line comments:**
```python
# This is a multi-line comment
# written using multiple
# single-line comment markers
```

**Example using a multi-line string (not recommended for actual comments):**
```python
"""
This is a multi-line string
that can act like a comment,
but it's technically a string.
"""
```

### Best Practices

- Use comments to explain **why** something is done, not just **what** is done.
- Keep comments concise and relevant.
- Avoid obvious comments that restate the code.

**Example:**
```python
# Bad comment
x = 10  # Set x to 10

# Good comment
x = 10  # Initial value used for loop counter
```

## Variables and Data Types

### Variables

Variables are used to store data in a program. In Python, you create a variable by assigning a value to a name using the `=` operator. Variable names should be descriptive and follow naming conventions (e.g., lowercase with underscores for readability).

**Example:**
```python
name = "Alice"
age = 30
is_active = True
```

Python is **dynamically typed**, meaning you don’t need to declare the type of a variable explicitly—Python infers it at runtime.

### Naming Rules

- Must start with a letter or underscore (`_`)
- Can contain letters, numbers, and underscores
- Cannot be a Python keyword (e.g., `if`, `class`, `def`)
- Case-sensitive (`score` and `Score` are different)

### Data Types

Python has several built-in data types. Here are some of the most commonly used:

#### Numeric Types

- `int`: Integer numbers  
  ```python
  count = 10
  ```
- `float`: Decimal numbers  
  ```python
  price = 19.99
  ```

#### Text Type

- `str`: A sequence of characters (string)  
  ```python
  message = "Hello, world!"
  ```

#### Boolean Type

- `bool`: Represents `True` or `False`  
  ```python
  is_valid = False
  ```

#### Sequence Types

- `list`: Ordered, mutable collection  
- `tuple`: Ordered, immutable collection  
- `range`: Sequence of numbers (often used in loops)

#### Mapping Type

- `dict`: Key-value pairs  
  ```python
  user = {"name": "Alice", "age": 30}
  ```

#### Set Types

- `set`, `frozenset`: Unordered collections of unique elements

#### None Type

- `None`: Represents the absence of a value  
  ```python
  result = None
  ```

### Type Checking

You can check the type of a variable using the `type()` function:

```python
x = 42
print(type(x))  # <class 'int'>
```

## Operators

Operators in Python are special symbols or keywords used to perform operations on variables and values. Python supports several types of operators, each serving a specific purpose.

### Arithmetic Operators

Used for basic mathematical operations.

| Operator | Description        | Example        |
|----------|--------------------|----------------|
| `+`      | Addition            | `3 + 2` → `5`  |
| `-`      | Subtraction         | `5 - 1` → `4`  |
| `*`      | Multiplication      | `4 * 2` → `8`  |
| `/`      | Division            | `10 / 2` → `5.0` |
| `//`     | Floor Division      | `7 // 2` → `3` |
| `%`      | Modulus (remainder) | `7 % 3` → `1`  |
| `**`     | Exponentiation      | `2 ** 3` → `8` |

### Comparison Operators

Used to compare values. They return a Boolean result (`True` or `False`).

| Operator | Description         | Example         |
|----------|---------------------|-----------------|
| `==`     | Equal to             | `5 == 5` → `True` |
| `!=`     | Not equal to         | `5 != 3` → `True` |
| `>`      | Greater than         | `7 > 4` → `True`  |
| `<`      | Less than            | `3 < 5` → `True`  |
| `>=`     | Greater than or equal| `5 >= 5` → `True` |
| `<=`     | Less than or equal   | `4 <= 6` → `True` |

### Logical Operators

Used to combine conditional statements.

| Operator | Description | Example                      |
|----------|-------------|------------------------------|
| `and`    | Logical AND | `True and False` → `False`   |
| `or`     | Logical OR  | `True or False` → `True`     |
| `not`    | Logical NOT | `not True` → `False`         |

### Assignment Operators

Used to assign values to variables.

| Operator | Description         | Example         |
|----------|---------------------|-----------------|
| `=`      | Assign               | `x = 5`         |
| `+=`     | Add and assign       | `x += 3` → `x = x + 3` |
| `-=`     | Subtract and assign  | `x -= 2`        |
| `*=`     | Multiply and assign  | `x *= 4`        |
| `/=`     | Divide and assign    | `x /= 2`        |
| `//=`    | Floor divide and assign | `x //= 2`    |
| `%=`     | Modulus and assign   | `x %= 3`        |
| `**=`    | Exponent and assign  | `x **= 2`       |

### Identity Operators

Used to compare memory locations of two objects.

| Operator | Description         | Example             |
|----------|---------------------|---------------------|
| `is`     | Same object          | `x is y`            |
| `is not` | Not the same object  | `x is not y`        |

### Membership Operators

Used to test if a value is in a sequence (like a list, string, or tuple).

| Operator | Description         | Example             |
|----------|---------------------|---------------------|
| `in`     | Value exists         | `'a' in 'apple'` → `True` |
| `not in` | Value does not exist | `'x' not in 'apple'` → `True` |

## User Input and Output

### Output with `print()`

The `print()` function is used to display output to the console. It can print strings, numbers, variables, and more.

**Examples:**
```python
print("Hello, world!")
print(42)
name = "Alice"
print("Name:", name)
```

You can also use **f-strings** for formatted output:
```python
age = 30
print(f"Alice is {age} years old.")
```

### Input with `input()`

The `input()` function is used to get input from the user. It always returns a string, so you may need to convert it to another type.

**Examples:**
```python
name = input("Enter your name: ")
print("Hello,", name)
```

To convert input to an integer or float:
```python
age = int(input("Enter your age: "))
height = float(input("Enter your height in meters: "))
```

### Combining Input and Output

You can combine both to create interactive programs:
```python
city = input("What city do you live in? ")
print(f"{city} sounds like a great place!")
```

## Namespaces

A namespace in Python is a container that holds a mapping between names (identifiers) and objects (values). It ensures that names are unique and can be used without conflict.

### Types of Namespaces

Python maintains several types of namespaces during execution:

- **Built-in Namespace**: Contains names like `print()`, `len()`, and `int()`. These are always available.
- **Global Namespace**: Contains names defined at the top level of a script or module.
- **Local Namespace**: Contains names defined inside a function.
- **Enclosing Namespace**: Refers to the namespace of any enclosing functions (used in nested functions).

### Example

```python
x = "global"

def outer():
    x = "enclosing"
    
    def inner():
        x = "local"
        print(x)
    
    inner()

outer()
```

This will print `"local"` because the innermost assignment takes precedence.

### The `LEGB` Rule

Python resolves names using the **LEGB** rule, which stands for:

- **L**ocal
- **E**nclosing
- **G**lobal
- **B**uilt-in

It searches for a name in this order and uses the first match it finds.

### The `globals()` and `locals()` Functions

- `globals()` returns a dictionary of the global namespace.
- `locals()` returns a dictionary of the local namespace.

```python
x = 10
print(globals()['x'])  # Outputs: 10
```

## Strings

A string in Python is a sequence of characters enclosed in either single quotes (`'`) or double quotes (`"`). Strings are used to represent text.

### Creating Strings

```python
greeting = "Hello"
name = 'Alice'
```

Triple quotes (`'''` or `"""`) can be used for multi-line strings:

```python
message = """This is
a multi-line
string."""
```

### String Indexing and Slicing

Strings are indexed starting at 0. You can access individual characters or slices (substrings) using square brackets.

```python
text = "Python"
print(text[0])     # 'P'
print(text[-1])    # 'n'
print(text[1:4])   # 'yth'
```

### String Methods

Python provides many built-in methods for string manipulation:

```python
s = "  hello world  "
print(s.upper())       # '  HELLO WORLD  '
print(s.strip())       # 'hello world'
print(s.replace("world", "Python"))  # '  hello Python  '
print(s.split())       # ['hello', 'world']
```

Common string methods include:
- `.lower()`, `.upper()`
- `.strip()`, `.lstrip()`, `.rstrip()`
- `.replace(old, new)`
- `.split(delimiter)`
- `.join(iterable)`
- `.find(substring)`, `.index(substring)`

### String Formatting

You can insert variables into strings using **f-strings**:

```python
name = "Alice"
age = 30
print(f"{name} is {age} years old.")
```

Other formatting methods include `.format()` and the `%` operator, though f-strings are preferred in modern Python.

### Escape Characters

Use a backslash `\` to include special characters in a string:

```python
quote = "She said, \"Hello!\""
newline = "Line1\nLine2"
```

### Immutability

Strings are **immutable**, meaning they cannot be changed after creation. Any operation that modifies a string returns a new string.

```python
s = "hello"
s = s.upper()  # creates a new string 'HELLO'
```

## Casting

Casting (also known as type conversion) is the process of converting a value from one data type to another. In Python, this is often done using built-in functions.

### Common Casting Functions

- `int()` – Converts a value to an integer
- `float()` – Converts a value to a floating-point number
- `str()` – Converts a value to a string
- `bool()` – Converts a value to a Boolean (`True` or `False`)

### Examples

```python
# String to int
num_str = "42"
num = int(num_str)  # 42

# Float to int (truncates decimal)
value = int(3.99)  # 3

# Int to float
x = float(7)  # 7.0

# Number to string
s = str(100)  # "100"

# Any value to boolean
print(bool(0))      # False
print(bool("text")) # True
```

If the value cannot be converted, Python will raise a `ValueError`:
  ```python
  int("abc")  # ValueError
  ```

Casting is useful when working with user input, which is always received as a string:
  ```python
  age = int(input("Enter your age: "))
  ```

## Boolean

A Boolean represents one of two values: `True` or `False`. These are used to perform logical operations and control the flow of programs.

### Boolean Values

```python
is_active = True
is_logged_in = False
```

Note: The first letter must be capitalized (`True`, not `true`).

### Boolean Expressions

Boolean expressions evaluate to either `True` or `False`. They are commonly used in conditions and comparisons.

```python
x = 10
print(x > 5)   # True
print(x == 7)  # False
```

### Truthy and Falsy Values

In Python, some values are treated as `True` or `False` in a Boolean context:

**Falsy values include:**
- `None`
- `False`
- `0`, `0.0`
- `''` (empty string)
- `[]`, `{}`, `set()` (empty collections)

Everything else is considered **truthy**.

```python
if []:
    print("This won't run")
if [1, 2, 3]:
    print("This will run")
```

### Logical Operators

Booleans are often used with logical operators:

```python
a = True
b = False

print(a and b)  # False
print(a or b)   # True
print(not a)    # False
```

## Lists

A list in Python is an ordered, mutable collection of items. Lists can store elements of any data type, including other lists.

### Creating Lists

Lists are defined using square brackets `[]`, with elements separated by commas.

```python
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, 3.14]
```

### Accessing Elements

You can access elements by their index (starting at 0):

```python
print(fruits[0])    # "apple"
print(fruits[-1])   # "cherry" (last item)
```

### Modifying Lists

Lists are mutable, meaning you can change their contents:

```python
fruits[1] = "blueberry"
```

You can also add or remove elements:

```python
fruits.append("orange")       # Add to end
fruits.insert(1, "kiwi")      # Insert at index
fruits.remove("apple")        # Remove by value
popped = fruits.pop()         # Remove last item
```

### List Slicing

You can extract parts of a list using slicing:

```python
numbers = [0, 1, 2, 3, 4, 5]
print(numbers[1:4])   # [1, 2, 3]
print(numbers[:3])    # [0, 1, 2]
print(numbers[::2])   # [0, 2, 4]
```

### Looping Through Lists

```python
for fruit in fruits:
    print(fruit)
```

### List Functions and Methods

- `len(list)` – Returns the number of elements
- `list.append(item)` – Adds an item to the end
- `list.extend(iterable)` – Adds multiple items
- `list.insert(index, item)` – Inserts at a position
- `list.remove(item)` – Removes first occurrence
- `list.pop([index])` – Removes and returns item
- `list.sort()` – Sorts the list in place
- `list.reverse()` – Reverses the list in place

### Nested Lists

Lists can contain other lists:

```python
matrix = [[1, 2], [3, 4]]
print(matrix[0][1])  # 2
```

## Tuples

A tuple is an ordered, immutable collection of items. Once created, the elements of a tuple cannot be changed.

### Creating Tuples

Tuples are defined using parentheses `()` with elements separated by commas. A single-element tuple must include a trailing comma.

```python
empty = ()
single = (42,)
numbers = (1, 2, 3)
mixed = ("hello", 3.14, True)
```

### Accessing Elements

You can access tuple elements by index, just like lists:

```python
print(numbers[0])    # 1
print(numbers[-1])   # 3
```

### Tuple Immutability

Tuples cannot be modified after creation:

```python
# This will raise an error
numbers[1] = 10
```

### Tuple Packing and Unpacking

You can pack values into a tuple and unpack them into variables:

```python
point = (3, 4)
x, y = point
print(x)  # 3
print(y)  # 4
```

### Tuple Functions

- `len(tuple)` – Returns the number of elements
- `tuple.count(value)` – Counts occurrences of a value
- `tuple.index(value)` – Returns the index of the first occurrence

## Range

The `range()` function in Python generates a sequence of numbers. It is commonly used in loops and for creating number sequences.

### Basic Usage

`range(stop)` generates numbers from `0` up to, but not including, `stop`.

```python
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4
```

### Specifying Start and Stop

You can specify both the starting and stopping values:

```python
for i in range(2, 6):
    print(i)  # 2, 3, 4, 5
```

### Specifying Step

You can also define the step (increment or decrement):

```python
for i in range(1, 10, 2):
    print(i)  # 1, 3, 5, 7, 9

for i in range(10, 0, -2):
    print(i)  # 10, 8, 6, 4, 2
```

### Converting to a List

To view the full sequence, convert the range to a list:

```python
numbers = list(range(5))
print(numbers)  # [0, 1, 2, 3, 4]
```

## Binary Type

Python provides built-in support for binary data using the `bytes`, `bytearray`, and `memoryview` types. These are useful for handling raw binary data, such as files, network communication, or image processing.

### Bytes

A `bytes` object is an immutable sequence of bytes.

```python
data = b"hello"
print(data[0])       # 104 (ASCII for 'h')
print(type(data))    # <class 'bytes'>
```

### Bytearray

A `bytearray` is a mutable version of `bytes`.

```python
data = bytearray(b"hello")
data[0] = 72
print(data)          # bytearray(b'Hello')
```

### Memoryview

A `memoryview` provides a view of the memory of another binary object without copying it.

```python
data = bytearray(b"hello")
view = memoryview(data)
print(view[1])       # 101 (ASCII for 'e')
```

### Converting to Bytes

You can convert strings or other data to bytes:

```python
text = "hello"
encoded = text.encode("utf-8")
print(encoded)       # b'hello'
```

### Use Cases

- Reading and writing binary files
- Network communication
- Efficient manipulation of large binary data

## NoneType

`NoneType` is the type of the special value `None`, which represents the absence of a value or a null value in Python.

### The `None` Object

`None` is often used to indicate:
- A default value for function arguments
- A placeholder for optional or missing data
- The return value of functions that don’t explicitly return anything

```python
result = None
print(result)         # None
print(type(result))   # <class 'NoneType'>
```

### Functions Returning `None`

If a function does not return a value explicitly, it returns `None` by default:

```python
def greet():
    print("Hello")

output = greet()
print(output)  # None
```

### Checking for `None`

Use `is` or `is not` to check for `None`:

```python
if result is None:
    print("No result yet")
```

## Dictionaries

A dictionary in Python is an unordered collection of key-value pairs. Each key must be unique and immutable, while values can be of any type.

### Creating Dictionaries

Dictionaries are defined using curly braces `{}` with key-value pairs separated by colons:

```python
person = {
    "name": "Alice",
    "age": 30,
    "is_student": False
}
```

You can also use the `dict()` constructor:

```python
person = dict(name="Bob", age=25)
```

### Accessing Values

Access values using keys:

```python
print(person["name"])       # "Alice"
print(person.get("age"))    # 30
```

The `get()` method returns `None` (or a default) if the key is not found:

```python
print(person.get("grade", "N/A"))  # "N/A"
```

### Modifying Dictionaries

You can add or update key-value pairs:

```python
person["age"] = 31
person["city"] = "New York"
```

### Removing Items

```python
del person["is_student"]
value = person.pop("age")
person.clear()  # Removes all items
```

### Looping Through Dictionaries

```python
for key in person:
    print(key, person[key])

for key, value in person.items():
    print(key, value)
```

### Dictionary Methods

- `dict.keys()` – Returns a view of keys
- `dict.values()` – Returns a view of values
- `dict.items()` – Returns a view of key-value pairs
- `dict.update(other_dict)` – Updates with another dictionary
- `dict.pop(key)` – Removes and returns the value for the key
- `dict.clear()` – Removes all items

## Datetime

The `datetime` module in Python provides classes for working with dates and times.

### Importing the Module

```python
import datetime
```

### Getting the Current Date and Time

```python
now = datetime.datetime.now()
print(now)  # e.g., 2025-06-10 10:00:00
```

### Creating Date and Time Objects

```python
date = datetime.date(2025, 6, 10)
time = datetime.time(14, 30, 0)
dt = datetime.datetime(2025, 6, 10, 14, 30)
```

### Accessing Components

```python
print(dt.year)     # 2025
print(dt.month)    # 6
print(dt.day)      # 10
print(dt.hour)     # 14
print(dt.minute)   # 30
```

### Formatting Dates and Times

Use `strftime()` to format a date/time as a string:

```python
formatted = dt.strftime("%Y-%m-%d %H:%M")
print(formatted)  # "2025-06-10 14:30"
```

### Parsing Strings into Dates

Use `strptime()` to convert a string into a `datetime` object:

```python
dt_str = "2025-06-10 14:30"
parsed = datetime.datetime.strptime(dt_str, "%Y-%m-%d %H:%M")
```

### Date Arithmetic

You can perform arithmetic with `timedelta`:

```python
from datetime import timedelta

tomorrow = now + timedelta(days=1)
yesterday = now - timedelta(days=1)
```

## if-else

The `if` statement is used to execute code based on a condition. You can use `elif` and `else` to handle multiple conditions.

### Basic if Statement

```python
x = 10
if x > 5:
    print("x is greater than 5")
```

### if-else Statement

```python
x = 3
if x > 5:
    print("x is greater than 5")
else:
    print("x is 5 or less")
```

### if-elif-else Chain

```python
x = 7
if x < 5:
    print("Less than 5")
elif x == 5:
    print("Equal to 5")
else:
    print("Greater than 5")
```

### Nested if Statements

```python
x = 10
if x > 0:
    if x < 20:
        print("x is between 1 and 19")
```

### Logical Operators

You can combine conditions using `and`, `or`, and `not`:

```python
x = 10
if x > 5 and x < 15:
    print("x is between 6 and 14")
```

## while

A `while` loop repeatedly executes a block of code as long as a given condition is `True`.

### Basic while Loop

```python
count = 0
while count < 5:
    print(count)
    count += 1
```

### Infinite Loop

Be careful with conditions that never become `False`:

```python
while True:
    print("This will run forever")
    break  # Use break to exit the loop
```

### Using break and continue

- `break` exits the loop immediately.
- `continue` skips the rest of the current iteration and moves to the next.

```python
x = 0
while x < 5:
    x += 1
    if x == 3:
        continue
    if x == 5:
        break
    print(x)
```

### else with while

The `else` block runs if the loop completes normally (not interrupted by `break`):

```python
x = 0
while x < 3:
    print(x)
    x += 1
else:
    print("Loop finished")
```

## for

A `for` loop is used to iterate over a sequence such as a list, tuple, string, or range.

### Basic for Loop

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

### Iterating Over a String

```python
for char in "hello":
    print(char)
```

### Using range()

```python
for i in range(3):
    print(i)  # 0, 1, 2
```

### Looping with Index

Use `enumerate()` to get both index and value:

```python
colors = ["red", "green", "blue"]
for index, color in enumerate(colors):
    print(index, color)
```

### Nested for Loops

```python
for i in range(2):
    for j in range(3):
        print(i, j)
```

### Using break and continue

```python
for i in range(5):
    if i == 3:
        continue
    if i == 4:
        break
    print(i)
```

### else with for

The `else` block runs if the loop completes without a `break`:

```python
for i in range(3):
    print(i)
else:
    print("Loop completed")
```

## function

Functions in Python are defined using the `def` keyword. They allow you to group code into reusable blocks.

### Defining a Function

```python
def greet():
    print("Hello!")
```

### Calling a Function

```python
greet()  # Output: Hello!
```

### Function with Parameters

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```

### Function with Return Value

```python
def add(a, b):
    return a + b

result = add(3, 4)
print(result)  # 7
```

### Default Parameter Values

```python
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet()           # Hello, Guest!
greet("Bob")      # Hello, Bob!
```

### Keyword Arguments

```python
def describe_pet(animal, name):
    print(f"{name} is a {animal}.")

describe_pet(name="Whiskers", animal="cat")
```

### Variable Number of Arguments

Use `*args` for positional arguments and `**kwargs` for keyword arguments:

```python
def add_all(*args):
    return sum(args)

print(add_all(1, 2, 3))  # 6

def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")
```

## lambda

A `lambda` function is a small anonymous function defined using the `lambda` keyword. It can have any number of arguments but only one expression.

### Basic Syntax

```python
# Equivalent to: def add(x, y): return x + y
add = lambda x, y: x + y
print(add(3, 4))  # 7
```

- `lambda x, y:` defines the parameters
- `x + y` is the expression that gets returned

### Using lambda with Built-in Functions

Lambda functions are often used with functions like `map()`, `filter()`, and `sorted()`.

```python
# Double each number in the list
nums = [1, 2, 3]
doubled = list(map(lambda x: x * 2, nums))
print(doubled)  # [2, 4, 6]
```

```python
# Filter out odd numbers
even = list(filter(lambda x: x % 2 == 0, nums))
print(even)  # [2]
```

```python
# Sort a list of tuples by the second element
pairs = [(1, 3), (2, 1), (4, 2)]
sorted_pairs = sorted(pairs, key=lambda x: x[1])
print(sorted_pairs)  # [(2, 1), (4, 2), (1, 3)]
```

### When to Use lambda

Use `lambda` for short, throwaway functions that are simple enough to define in-line. For more complex logic, use a regular `def` function.

## arrays

Python does not have a built-in array type like some other languages, but the `array` module provides a space-efficient array implementation for basic numeric types.

> Note: For more advanced array operations (especially in data science), the `numpy` library is commonly used, but that is typically covered separately.

### Importing the array Module

```python
import array
```

### Creating an Array

Use `array.array(typecode, initializer)` where `typecode` specifies the data type.

```python
import array

# Create an array of integers
numbers = array.array('i', [1, 2, 3, 4])
print(numbers)  # array('i', [1, 2, 3, 4])
```

Common typecodes:
- `'i'` – signed integer
- `'f'` – float
- `'d'` – double-precision float

### Accessing and Modifying Elements

```python
print(numbers[0])  # 1

numbers[1] = 10    # Change second element
print(numbers)     # array('i', [1, 10, 3, 4])
```

### Looping Through an Array

```python
for num in numbers:
    print(num)
```

### Adding and Removing Elements

```python
numbers.append(5)         # Add to end
numbers.insert(1, 99)     # Insert at index 1
numbers.pop()             # Remove last element
numbers.remove(99)        # Remove first occurrence of 99
```

### Array Methods

- `append(x)` – Adds an item to the end
- `insert(i, x)` – Inserts item at index `i`
- `pop([i])` – Removes and returns item at index `i` (last if not specified)
- `remove(x)` – Removes first occurrence of `x`
- `index(x)` – Returns index of first occurrence
- `reverse()` – Reverses the array in place
- `buffer_info()` – Returns memory address and length

## classes and objects

Python is an object-oriented programming language, which means it allows you to define your own data types using classes. Objects are instances of these classes.

### Defining a Class

Use the `class` keyword to define a class:

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # instance variable
        self.age = age

    def greet(self):
        print(f"Hello, my name is {self.name}.")
```

- `__init__` is the constructor method, called when a new object is created.
- `self` refers to the current instance of the class.

### Creating an Object

```python
p1 = Person("Alice", 30)  # Create an instance of Person
p1.greet()                # Output: Hello, my name is Alice.
```

### Accessing Attributes and Methods

```python
print(p1.name)  # Access attribute: Alice
print(p1.age)   # Access attribute: 30
p1.greet()      # Call method
```

### Modifying Attributes

```python
p1.age = 31
print(p1.age)  # 31
```

### Adding Methods

You can define additional methods inside the class to perform actions:

```python
class Person:
    def __init__(self, name):
        self.name = name

    def say_hello(self):
        return f"Hi, I'm {self.name}!"
```

### Deleting Attributes or Objects

```python
del p1.age       # Deletes the age attribute
del p1           # Deletes the object
```

## OOP Concepts: Inheritance, Abstraction, Polymorphism, Encapsulation

Python supports Object-Oriented Programming (OOP), which is based on the concept of "objects" that bundle data and behavior together. Here are four core OOP principles:

### Inheritance

Inheritance allows a class (child) to inherit attributes and methods from another class (parent).

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):  # Dog inherits from Animal
    def speak(self):
        print("Dog barks")

d = Dog()
d.speak()  # Output: Dog barks
```

### Abstraction

Abstraction hides complex implementation details and shows only the essential features. In Python, this is often done using abstract base classes.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass  # Must be implemented by subclasses

class Circle(Shape):
    def area(self):
        return 3.14 * 5 * 5  # Example with fixed radius

c = Circle()
print(c.area())
```

### Polymorphism

Polymorphism allows different classes to be treated through a common interface, even if they implement behavior differently. This is often done using inheritance and method overriding.

```python
from abc import ABC, abstractmethod

# Abstract base class
class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass  # Must be implemented by subclasses

# Subclass 1
class Cat(Animal):
    def sound(self):
        print("Meow")

# Subclass 2
class Dog(Animal):
    def sound(self):
        print("Bark")

# Polymorphic behavior
animals = [Cat(), Dog()]
for animal in animals:
    animal.sound()  # Calls the appropriate overridden method
```

- `Animal` defines a common interface with the `sound()` method.
- `Cat` and `Dog` provide their own implementations of `sound()`.
- The loop treats all objects as `Animal` but calls the correct method based on the actual object type.


### Encapsulation

Encapsulation restricts direct access to some of an object's components, usually by using private variables and methods.

```python
class Person:
    def __init__(self, name):
        self.__name = name  # Private attribute

    def get_name(self):
        return self.__name  # Public method to access private data

p = Person("Alice")
print(p.get_name())  # Alice
```

- Prefixing with `__` makes an attribute private (name mangling).
- Use getter/setter methods to access or modify private data.

## inheritance

Inheritance allows a class (child or subclass) to acquire properties and behaviors (methods and attributes) from another class (parent or superclass). This promotes code reuse and logical hierarchy.

### Basic Inheritance

```python
# Parent class
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound")

# Child class
class Dog(Animal):
    def speak(self):
        print(f"{self.name} barks")

d = Dog("Buddy")
d.speak()  # Output: Buddy barks
```

- `Dog` inherits from `Animal` and overrides the `speak()` method.
- The `__init__` method from `Animal` is reused in `Dog`.

### Using super()

The `super()` function allows you to call methods from the parent class.

```python
class Cat(Animal):
    def __init__(self, name, color):
        super().__init__(name)  # Call parent constructor
        self.color = color

    def describe(self):
        print(f"{self.name} is a {self.color} cat")
```

### Multi-Level Inheritance

```python
# Base class
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def start(self):
        print(f"{self.brand} vehicle is starting")

# Intermediate class
class Car(Vehicle):
    def drive(self):
        print(f"{self.brand} car is driving")

# Derived class
class ElectricCar(Car):
    def charge(self):
        print(f"{self.brand} electric car is charging")

# Create an instance of ElectricCar
car = ElectricCar("Some EV Brand")
car.start()   # Inherited from Vehicle
car.drive()   # Inherited from Car
car.charge()  # Defined in ElectricCar
```


### Checking Inheritance

```python
print(isinstance(car, ElectricCar))   # True
print(isinstance(car, Car))  # True
print(issubclass(ElectricCar, Car))  # True
```
## iterators

An **iterator** is an object that represents a stream of data; it returns one element at a time when you call `next()` on it. Iterators are used in loops and other iterable contexts.

### Iterable vs Iterator

- **Iterable**: An object capable of returning its members one at a time (e.g., list, tuple, string).
- **Iterator**: An object with a `__next__()` method and an `__iter__()` method that returns itself.

### Using an Iterator

```python
nums = [1, 2, 3]
it = iter(nums)  # Get an iterator from the list

print(next(it))  # 1
print(next(it))  # 2
print(next(it))  # 3
# next(it) now would raise StopIteration
```

### Creating a Custom Iterator

You can create your own iterator by defining a class with `__iter__()` and `__next__()` methods.

```python
class CountDown:
    def __init__(self, start):
        self.num = start

    def __iter__(self):
        return self  # The iterator object returns itself

    def __next__(self):
        if self.num <= 0:
            raise StopIteration
        current = self.num
        self.num -= 1
        return current

cd = CountDown(3)
for number in cd:
    print(number)  # 3, 2, 1
```

- `__iter__()` returns the iterator object itself.
- `__next__()` returns the next value and raises `StopIteration` when done.

## scope

**Scope** defines where in your code a variable is accessible. It determines the visibility of a name, while a **namespace** is the actual mapping between names and objects.

### Scope vs Namespace

- **Scope** is about **where** a name can be used.
- **Namespace** is about **how** names are stored and organized (like a dictionary).

Python uses the **LEGB rule** to resolve variable names by searching through different scopes in a specific order.

### LEGB Rule

1. **Local** – Inside the current function
2. **Enclosing** – In the local scope of any enclosing functions
3. **Global** – At the top level of the script or module
4. **Built-in** – Predefined names like `len`, `print`, etc.

### Local Scope

Defined inside a function and only accessible there.

```python
def greet():
    name = "Alice"  # Local to greet()
    print(name)

greet()
# print(name)  # Error: name is not defined outside the function
```

### Global Scope

Defined at the top level of a script or module.

```python
x = 10  # Global variable

def show():
    print(x)  # Accesses global x

show()
```

### Modifying Global Variables

Use the `global` keyword to modify a global variable inside a function.

```python
count = 0

def increment():
    global count
    count += 1

increment()
print(count)  # 1
```

### Enclosing Scope (Nested Functions)

A function defined inside another function can access variables from the outer function.

```python
def outer():
    msg = "Hello"

    def inner():
        print(msg)  # Accesses enclosing scope

    inner()

outer()
```

### Built-in Scope

Includes names that are always available in Python.

```python
print(len("hello"))  # 5
```

### Summary

- A **namespace** is a system that maintains the association between names and the objects they refer to. It organizes all the identifiers (like variable names, function names, etc.) in a given context.
- A **scope** is the region of the code where a namespace is directly accessible. It determines which namespace Python will search when you reference a name.

## Module

A module in Python is a file containing Python definitions and statements. Modules help organize code into manageable sections and promote reusability.

### Creating and Using Modules

You can create a module by saving Python code in a `.py` file. To use a module, import it into another script.

```python
# mymodule.py
def greet(name):
    return f"Hello, {name}!"
```

```python
# main.py
import mymodule

print(mymodule.greet("Alice"))
```

### Importing Specific Items

You can import specific functions or variables from a module:

```python
from mymodule import greet

print(greet("Bob"))
```

### Renaming Modules

Modules can be imported with an alias:

```python
import mymodule as mm

print(mm.greet("Charlie"))
```

### Built-in Modules

Python includes many built-in modules, such as `math`, `random`, and `datetime`.

```python
import math

print(math.sqrt(16))  # 4.0
```

### Checking Module Contents

Use `dir()` to list all attributes of a module:

```python
import math

print(dir(math))
```

### Module Search Path

Python searches for modules in the directories listed in `sys.path`.

```python
import sys

print(sys.path)
```

## Math

Python provides several ways to perform mathematical operations, including built-in operators and the `math` module for advanced functions.

### Using the `math` Module

The `math` module provides access to common mathematical functions and constants.

```python
import math

print(math.sqrt(16))        # 4.0
print(math.pow(2, 3))       # 8.0
print(math.factorial(5))    # 120
print(math.gcd(12, 18))     # 6
```

### Trigonometric Functions

```python
print(math.sin(math.pi / 2))  # 1.0
print(math.cos(0))            # 1.0
print(math.tan(math.pi / 4))  # 1.0
```

### Constants

```python
print(math.pi)    # 3.141592653589793
print(math.e)     # 2.718281828459045
```

### Rounding and Logarithms

```python
print(math.ceil(2.3))     # 3
print(math.floor(2.7))    # 2
print(math.log(100, 10))  # 2.0
print(math.log10(1000))   # 3.0
```

## Logging

The `logging` module in Python provides a flexible way to track events that happen during program execution. It is useful for debugging and monitoring applications.

### Basic Logging

```python
import logging

logging.basicConfig(level=logging.INFO)
logging.info("This is an info message")
```

### Logging Levels

- `DEBUG` – Detailed information, typically for diagnosing problems.
- `INFO` – Confirmation that things are working as expected.
- `WARNING` – An indication that something unexpected happened.
- `ERROR` – A more serious problem.
- `CRITICAL` – A very serious error.

```python
logging.debug("Debug message")
logging.info("Info message")
logging.warning("Warning message")
logging.error("Error message")
logging.critical("Critical message")
```

### Customizing Log Format

```python
logging.basicConfig(
    level=logging.DEBUG,
    format="%(asctime)s - %(levelname)s - %(message)s"
)
```

### Logging to a File

```python
logging.basicConfig(
    filename="app.log",
    level=logging.WARNING,
    format="%(asctime)s - %(levelname)s - %(message)s"
)
```

### Disabling Logging

```python
logging.disable(logging.CRITICAL)
```

## JSON

JSON (JavaScript Object Notation) is a lightweight data format used for storing and exchanging data. Python provides the `json` module to work with JSON data.

### Importing the Module

```python
import json
```

### Converting Python to JSON

Use `json.dumps()` to convert Python objects into JSON strings.

```python
data = {"name": "Alice", "age": 25, "is_student": False}
json_string = json.dumps(data)

print(json_string)  # '{"name": "Alice", "age": 25, "is_student": false}'
```

### Converting JSON to Python

Use `json.loads()` to parse a JSON string into a Python object.

```python
json_data = '{"name": "Bob", "age": 30}'
parsed = json.loads(json_data)

print(parsed["name"])  # "Bob"
```

### What `load` and `loads` Return

The return type depends on the JSON structure:

- JSON object → Python `dict`
- JSON array → Python `list`
- JSON string → Python `str`
- JSON number → Python `int` or `float`
- JSON `true`/`false` → Python `True`/`False`
- JSON `null` → Python `None`

```python
print(json.loads('{"a": 1}'))       # {'a': 1} (dict)
print(json.loads('[1, 2, 3]'))      # [1, 2, 3] (list)
print(json.loads('"hello"'))       # 'hello' (str)
print(json.loads('true'))          # True (bool)
print(json.loads('null'))          # None
```

### Working with JSON Files

#### Writing to a JSON File

```python
with open("data.json", "w") as file:
    json.dump(data, file)
```

#### Reading from a JSON File

```python
with open("data.json", "r") as file:
    loaded_data = json.load(file)

print(loaded_data)
```

### Formatting Options

You can make JSON output more readable using `indent` and `sort_keys`.

```python
print(json.dumps(data, indent=4, sort_keys=True))
```

## Regex

Regex (short for *regular expression*) is a powerful tool for matching patterns in text. Python provides the `re` module to work with regular expressions.

### Importing the Module

```python
import re
```

### Basic Pattern Matching

Use `re.search()` to find the first match of a pattern in a string.

```python
text = "The price is $100"
match = re.search(r"\$\d+", text)

if match:
    print(match.group())  # $100
```

### Finding All Matches

Use `re.findall()` to return all non-overlapping matches.

```python
text = "Email: alice@example.com, bob@example.org"
emails = re.findall(r"\b\w+@\w+\.\w+\b", text)

print(emails)  # ['alice@example.com', 'bob@example.org']
```

### Replacing Text

Use `re.sub()` to replace parts of a string that match a pattern.

```python
text = "123-456-7890"
cleaned = re.sub(r"-", "", text)

print(cleaned)  # 1234567890
```

### Splitting Strings

Use `re.split()` to split a string by a regex pattern.

```python
text = "apple, banana; orange"
fruits = re.split(r"[;,]\s*", text)

print(fruits)  # ['apple', 'banana', 'orange']
```

### Common Regex Patterns

- `\d` – Digit
- `\w` – Word character (letters, digits, underscore)
- `\s` – Whitespace
- `.` – Any character except newline
- `*` – Zero or more
- `+` – One or more
- `?` – Zero or one
- `^` – Start of string
- `$` – End of string
- `[]` – Character set
- `()` – Grouping

### Compiling Patterns

For repeated use, compile a regex pattern:

```python
pattern = re.compile(r"\d+")
print(pattern.findall("There are 3 cats and 4 dogs"))
```

## pip and Install pip

`pip` is the package installer for Python. It allows you to install and manage additional libraries and dependencies that are not part of the standard library.

### Installing Packages with pip

Use the `pip install` command to install packages from the Python Package Index (PyPI).

```bash
pip install requests
```

### Installing Specific Versions

```bash
pip install requests==2.31.0
```

### Upgrading Packages

```bash
pip install --upgrade requests
```

### Uninstalling Packages

```bash
pip uninstall requests
```

### Listing Installed Packages

```bash
pip list
```

### Checking Package Info

```bash
pip show requests
```

### Installing from a Requirements File

A `requirements.txt` file lists packages to install.

```bash
pip install -r requirements.txt
```

### Installing pip

Most Python distributions come with `pip` pre-installed. If it's missing, you can install it using:

```bash
python -m ensurepip --upgrade
```

Or download the `get-pip.py` script and run:

```bash
python get-pip.py
```

## pylint

`pylint` is a static code analysis tool for Python. It checks for errors, enforces coding standards, and suggests improvements to make your code more readable and maintainable.

### Installing pylint

```bash
pip install pylint
```

### Running pylint

To analyze a Python file:

```bash
pylint my_script.py
```

### Sample Output

`pylint` provides a score out of 10 and lists messages such as:

- Convention (`C`) – Coding style issues
- Refactor (`R`) – Suggestions for code structure
- Warning (`W`) – Potential problems
- Error (`E`) – Likely bugs

Example:

```
************* Module my_script
my_script.py:1:0: C0114: Missing module docstring (missing-module-docstring)
my_script.py:2:0: C0103: Variable name "x" doesn't conform to snake_case naming style (invalid-name)
```

### Common Options

- `--disable=<msg-id>` – Disable specific messages
- `--max-line-length=100` – Set maximum line length
- `--output-format=json` – Change output format

Example:

```bash
pylint my_script.py --disable=C0114 --max-line-length=100
```

### Configuration File

You can create a `.pylintrc` file to customize settings:

```bash
pylint --generate-rcfile > .pylintrc
```

#### Example `.pylintrc` Settings

```ini
[MASTER]
ignore=venv
jobs=1

[MESSAGES CONTROL]
disable=C0114, C0115, C0116  # Disable missing docstring warnings

[FORMAT]
max-line-length=100
indent-string='    '

[DESIGN]
max-args=5
max-locals=15
max-returns=6

[REPORTS]
output-format=colorized
```

This configuration:
- Ignores the `venv` directory
- Disables docstring warnings
- Sets max line length to 100
- Limits function arguments and local variables
- Uses colorized output for readability

## Error

In Python, an error is an issue in a program that causes it to stop execution. Errors are broadly categorized into **syntax errors** and **runtime errors**.

### Syntax Errors

These occur when the Python parser detects incorrect syntax. They prevent the code from running.

```python
# Missing colon
if True
    print("Hello")
```

### Runtime Errors

These occur while the program is running. They are also known as **exceptions**.

```python
# Division by zero
x = 10 / 0
```

### Common Error Types

- `SyntaxError`: Invalid Python syntax
- `NameError`: Using a variable that hasn’t been defined
- `TypeError`: Operation applied to an inappropriate type
- `IndexError`: Index out of range for a sequence
- `KeyError`: Accessing a non-existent dictionary key
- `ValueError`: Function receives an argument of the right type but inappropriate value
- `ZeroDivisionError`: Division by zero

### Viewing Error Messages

Python provides a traceback when an error occurs, showing where the error happened:

```python
numbers = [1, 2, 3]
print(numbers[5])  # IndexError
```

**Output:**
```
Traceback (most recent call last):
  File "example.py", line 2, in <module>
    print(numbers[5])
IndexError: list index out of range
```

## Exception Handling

Exception handling in Python allows you to manage runtime errors gracefully without crashing the program. This is done using `try`, `except`, and optionally `else` and `finally` blocks.

### Basic try-except

Use `try` to wrap code that might raise an exception, and `except` to handle the error:

```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero.")
```

### Catching Multiple Exceptions

You can handle different exceptions separately:

```python
try:
    value = int("abc")
except ValueError:
    print("Invalid input: not a number.")
except TypeError:
    print("Type error occurred.")
```

### Catching All Exceptions

Use a generic `except` to catch any exception (not recommended for debugging):

```python
try:
    risky_code()
except Exception as e:
    print("An error occurred:", e)
```

### else Block

The `else` block runs if no exceptions occur:

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Error!")
else:
    print("Success:", result)
```

### finally Block

The `finally` block always runs, whether an exception occurred or not. It's useful for cleanup actions:

```python
try:
    file = open("data.txt")
except FileNotFoundError:
    print("File not found.")
finally:
    print("Execution complete.")
```

## File Handling

Python provides built-in functions to work with files, allowing you to read from, write to, and manage files on your system.

### Opening Files

Use the `open()` function to open a file. It returns a file object.

```python
file = open("example.txt", "r")  # Open for reading
```

### File Modes

- `"r"` – Read (default)
- `"w"` – Write (creates or overwrites)
- `"a"` – Append
- `"x"` – Create (fails if file exists)
- `"b"` – Binary mode
- `"t"` – Text mode (default)

You can combine modes, e.g., `"rb"` for reading binary.

### Closing Files

Always close files to free up system resources:

```python
file.close()
```

Or use a `with` block to handle it automatically:

```python
with open("example.txt", "r") as file:
    content = file.read()
```

### Reading Files

```python
with open("example.txt", "r") as file:
    print(file.read())        # Read entire file
    # print(file.readline())  # Read one line
    # print(file.readlines()) # Read all lines into a list
```

### Writing to Files

```python
with open("example.txt", "w") as file:
    file.write("Hello, world!")
```

Use `"a"` mode to append instead of overwrite:

```python
with open("example.txt", "a") as file:
    file.write("\nAnother line.")
```

## Read Files

Reading files in Python allows you to access and process data stored in external text or binary files. This is commonly used for configuration files, logs, datasets, and more.

### Opening a File for Reading

Use the `open()` function with mode `"r"` (read mode):

```python
file = open("example.txt", "r")
```

Always close the file when done:

```python
file.close()
```

### Using `with` Statement

The `with` statement is preferred because it automatically handles closing the file:

```python
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
```

### Reading Methods

#### `read()`

Reads the entire file as a single string:

```python
with open("example.txt", "r") as file:
    data = file.read()
    print(data)
```

#### `readline()`

Reads one line at a time (including the newline character):

```python
with open("example.txt", "r") as file:
    line1 = file.readline()
    line2 = file.readline()
    print(line1, line2)
```

#### `readlines()`

Reads all lines into a list:

```python
with open("example.txt", "r") as file:
    lines = file.readlines()
    print(lines)
```

### Iterating Over Lines

You can loop through a file line by line:

```python
with open("example.txt", "r") as file:
    for line in file:
        print(line.strip())  # Removes newline characters
```

### Reading in Chunks

Useful for large files:

```python
with open("large_file.txt", "r") as file:
    while chunk := file.read(1024):  # Read 1024 characters at a time
        print(chunk)
```

### Handling File Paths

Use raw strings or `os.path` for cross-platform compatibility:

```python
import os

path = os.path.join("folder", "example.txt")
with open(path, "r") as file:
    print(file.read())
```

## Write/Create Files

Python allows you to create and write to files using the built-in `open()` function with write (`"w"`), append (`"a"`), or exclusive creation (`"x"`) modes.

### Writing to a File

Use `"w"` mode to write to a file. If the file exists, it will be **overwritten**.

```python
with open("output.txt", "w") as file:
    file.write("This is the first line.\n")
    file.write("This will overwrite any existing content.\n")
```

### Appending to a File

Use `"a"` mode to **add content to the end** of an existing file without deleting its contents.

```python
with open("output.txt", "a") as file:
    file.write("This line is appended.\n")
```

### Creating a New File

Use `"x"` mode to create a new file. If the file already exists, it raises a `FileExistsError`.

```python
try:
    with open("newfile.txt", "x") as file:
        file.write("This file was just created.")
except FileExistsError:
    print("File already exists.")
```

### Writing Multiple Lines

You can write multiple lines using `writelines()`, which takes a list of strings:

```python
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
with open("multilines.txt", "w") as file:
    file.writelines(lines)
```

### Writing with String Formatting

You can use f-strings or `.format()` to dynamically write content:

```python
name = "Alice"
score = 95

with open("report.txt", "w") as file:
    file.write(f"Student: {name}\nScore: {score}\n")
```

### Writing Binary Files

Use `"wb"` mode to write binary data (e.g., images, encoded content):

```python
data = bytes([120, 3, 255, 0, 100])
with open("binary.dat", "wb") as file:
    file.write(data)
```

### Best Practices

- Always use `with` to ensure files are properly closed.
- Be cautious with `"w"` mode—it will erase existing content.
- Use `"a"` for logging or appending data.
- Handle exceptions when creating files to avoid overwriting or crashing.

## Delete Files

Python provides tools to delete files and directories using the `os` and `pathlib` modules. This is useful for cleaning up temporary files, logs, or outdated data.

### Using `os.remove()`

The `os` module allows you to delete a file by specifying its path:

```python
import os

if os.path.exists("old_file.txt"):
    os.remove("old_file.txt")
else:
    print("File does not exist.")
```

### Using `pathlib.Path.unlink()`

The `pathlib` module offers an object-oriented approach:

```python
from pathlib import Path

file_path = Path("old_file.txt")
if file_path.exists():
    file_path.unlink()
```

### Handling Exceptions

Always handle exceptions to avoid crashes if the file doesn't exist or is in use:

```python
try:
    os.remove("important.txt")
except FileNotFoundError:
    print("File not found.")
except PermissionError:
    print("Permission denied.")
```

### Deleting Empty Directories

Use `os.rmdir()` to delete an empty folder:

```python
os.rmdir("empty_folder")
```

### Deleting Non-Empty Directories

Use `shutil.rmtree()` to delete a folder and all its contents:

```python
import shutil

shutil.rmtree("folder_to_delete")
```

Be cautious with `os.remove()` and `shutil.rmtree()` — deleted files and folders cannot be recovered through Python.

### Best Practices

- Always check if the file or directory exists before deleting.
- Use exception handling to manage errors gracefully.
- Avoid hardcoding paths; use `os.path` or `pathlib` for portability.

## Unit Testing

Unit testing is the process of testing individual units of code (usually functions or methods) to ensure they work as expected. Python provides a built-in module called `unittest` for writing and running tests.

### Why Unit Testing?

- Helps catch bugs early
- Makes code easier to maintain and refactor
- Documents expected behavior
- Supports test-driven development (TDD)

### Basic Structure

A unit test is written as a class that inherits from `unittest.TestCase`. Each test method should start with `test_`.

```python
import unittest

def add(a, b):
    return a + b

class TestMathFunctions(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)

if __name__ == "__main__":
    unittest.main()
```

### Common Assertions

- `assertEqual(a, b)` – Check if `a == b`
- `assertNotEqual(a, b)` – Check if `a != b`
- `assertTrue(x)` – Check if `x` is `True`
- `assertFalse(x)` – Check if `x` is `False`
- `assertIsNone(x)` – Check if `x is None`
- `assertIn(a, b)` – Check if `a in b`
- `assertRaises(Error, func, *args)` – Check if an error is raised

### Running Tests

You can run tests by executing the script directly or using the command line:

```bash
python -m unittest test_module.py
```

### Organizing Tests

- Place tests in a separate file or directory (e.g., `tests/`)
- Use descriptive names for test functions
- Group related tests into classes

### Example: Testing a Function

```python
def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero.")
    return a / b

class TestDivide(unittest.TestCase):
    def test_divide_normal(self):
        self.assertEqual(divide(10, 2), 5)

    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            divide(10, 0)
```