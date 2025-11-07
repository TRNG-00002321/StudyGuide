# Python Study Guide - Part 2

## Garbage Collection

Garbage Collection in Python is an automatic process that handles memory allocation and deallocation, ensuring efficient use of memory. Python automatically manages memory through two primary strategies:

1. Reference counting
2. Garbage collection

**Reference counting**
Python uses reference counting to manage memory. Each object keeps track of how many references point to it. When the reference count drops to zero i.e., no references remain, Python automatically deallocates the object.

```python
import sys

x = [1, 2, 3]
print(sys.getrefcount(x))

y = x
print(sys.getrefcount(x))

y = None
print(sys.getrefcount(x))
```

**Problem with Reference Counting**
Reference counting fails in the presence of cyclic references i.e., objects that reference each other in a cycle. Even if nothing else points to them, their reference count never reaches zero.

```python
import sys
x = [1, 2, 3]
y = [4, 5, 6]

x.append(y)
y.append(x)
print(sys.getrefcount(x))
print(sys.getrefcount(y))
```

**Garbage collection for Cyclic References**
Garbage collection is a memory management technique used in programming languages to automatically reclaim memory that is no longer accessible or in use by the application. To handle such circular references, Python uses a Garbage Collector (GC) from the built-in gc module. This collector is able to detect and clean up objects involved in reference cycles.

**Generational Garbage Collection**
Python’s Generational Garbage Collector is designed to deal with cyclic references. It organizes objects into three generations based on their lifespan:

- Generation 0: Newly created objects.
- Generation 1: Objects that survived one collection cycle.
- Generation 2: Long-lived objects.

When reference cycles occur, the garbage collector automatically detects and cleans them up, freeing the memory.

**Manual garbage collection**
Sometimes it’s beneficial to manually invoke the garbage collector, especially in the case of reference cycles.

```python
import gc

# Create a cycle
def fun(i):
    x = {}
    x[i + 1] = x
    return x

# Trigger garbage collection
c = gc.collect()
print(c)

for i in range(10):
    fun(i)

c = gc.collect()
print(c)
```

**Disabling garbage collection**
In Python, the garbage collector runs automatically to clean up unreferenced objects. To prevent it from running, you can disable it using gc.disable() from the gc module.

## Dunder or magic methods in Python
Dunder methods, also known as "magic methods" in Python, are special methods that have double underscores at the beginning and end of their names (e.g.,` __init__, __add__, __str__`). These methods are not meant to be invoked directly by the programmer; instead, they are called internally by the Python interpreter in response to certain actions, such as using operators or built-in functions. 

**1. `__init__ ` method
The `__init__` method for initialization is invoked without any call, when an instance of a class is created, like constructors in certain other programming languages such as C++, Java, C#, PHP, etc.

**2. ` __repr__ `method** (for devlopers)
`__repr__ ` method in Python defines how an object is presented as a string.

**3. `__str__`** (for users): This method is intended to return a "user-friendly" or "human-readable" string representation of an object.

## String Interning in Python
String interning is a memory optimization technique used in Python to enhance the efficiency of string handling. In Python, strings are immutable, meaning their values cannot be changed after creation. String interning, or interning strings, involves reusing existing string objects rather than creating new ones with the same value. This process can lead to memory savings and improved performance in certain scenarios.

## List Comprehension
List comprehension offers a shorter syntax when you want to create a new list based on the values of an existing list.

Without list comprehension you will have to write a for statement with a conditional test inside:
```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = []

for x in fruits:
  if "a" in x:
    newlist.append(x)

print(newlist)
```

With list comprehension you can do all that with only one line of code:
```python
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]

newlist = [x for x in fruits if "a" in x]

print(newlist)
```

**The Syntax**
`newlist = [expression for item in iterable if condition == True]`
The return value is a new list, leaving the old list unchanged.

**Condition**
The condition is like a filter that only accepts the items that evaluate to True.

## map filter and reduce function
Python's map(), filter(), and reduce() functions are tools for functional programming, enabling concise and efficient data manipulation.

## map(function, iterable)
Applies a given function to each item in an iterable (e.g., a list, tuple, or string) and returns a map object, which is an iterator containing the results.
```python
    numbers = [1, 2, 3, 4]
    squared_numbers = list(map(lambda x: x**2, numbers))
    print(squared_numbers)
    # Output: [1, 4, 9, 16]
```

## filter(function, iterable)
Constructs an iterator from elements of an iterable for which the given function returns True. The function must return a boolean value.
```python
    numbers = [1, 2, 3, 4, 5, 6]
    even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
    print(even_numbers)
    # Output: [2, 4, 6]
```

## reduce(function, iterable[, initializer])
Applies a function of two arguments cumulatively to the items of an iterable from left to right, reducing the iterable to a single value. It requires importing from the functools module.
```python
    from functools import reduce

    numbers = [1, 2, 3, 4]
    product = reduce(lambda x, y: x * y, numbers)
    print(product)
    # Output: 24 (1 * 2 * 3 * 4)
```

## Key Differences:
**map()** transforms each element individually, returning a new iterable of the same length.
**filter()** selects elements based on a condition, returning a new iterable with potentially fewer elements.
**reduce()** aggregates elements into a single value.

## Zip Function
The zip() function in Python is a built-in utility that combines multiple iterable objects (like lists, tuples, or strings) into a single iterable of tuples. It pairs corresponding elements from each input iterable based on their index. 

```python
names = ["Alice", "Bob", "Charlie"]
ages = [30, 24, 35]

combined_data = zip(names, ages)
print(list(combined_data))
```
```python
#Output
[('Alice', 30), ('Bob', 24), ('Charlie', 35)]
```

```python
fruits = ["apple", "banana", "cherry"]
prices = [1.0, 0.5]

zipped_items = zip(fruits, prices)
print(list(zipped_items))
```

```python
#Output
[('apple', 1.0), ('banana', 0.5)]
```

## Unzipping
You can effectively "unzip" a zipped object using the * (unpacking) operator with zip() again.

```python
zipped_data = [('Alice', 30), ('Bob', 24)]
unzipped_names, unzipped_ages = zip(*zipped_data)

print(unzipped_names)
print(unzipped_ages)

#Output
('Alice', 'Bob')
(30, 24)
```
##  Creating Dictionaries:
zip() is commonly used to create dictionaries from two lists: one for keys and one for values.
```python
keys = ["name", "age", "city"]
values = ["David", 40, "New York"]

person_dict = dict(zip(keys, values))
print(person_dict)

#Output
{'name': 'David', 'age': 40, 'city': 'New York'}
```

## Generator Expressions
In Python, generators provide a convenient way to implement the iterator protocol. Generator is an iterable created using a function with a yield statement.
The main feature of generator expression is evaluating the elements on demand. When you call a normal function with a return statement the function is terminated whenever it encounters a return statement. In a function with a yield statement the state of the function is “saved” from the last call and can be picked up the next time you call a generator function.

A Python generator expression is an expression that returns a generator (generator object).
Generator expression in Python allows creating a generator on a fly without a yield keyword. 
The syntax and concept is similar to list comprehensions
In terms of syntax, the only difference is that you use parentheses instead of square brackets. However, the types of data returned by Python generator expressions and list comprehensions differ. The main advantage of generator over a list is that it takes much less memory.

```python
gen_exp = (x ** 2 for x in range(10) if x % 2 == 0)
for x in gen_exp:
    print(x)

#Output
4
16
36
64
```



