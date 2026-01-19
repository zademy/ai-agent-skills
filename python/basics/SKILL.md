---
name: basics
description: >
  Python basics.
  Trigger: When working with Python - variables, types, operators, control flow, functions
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Python Basics / Core"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Python Basics

## Variables y Types  in datos

```python
# Variables
name = "John"          # str
age = 30               # int
height = 1.75          # float
is_active = True       # bool

# Multiple assignment
a, b, c = 1, 2, 3

# Constants
MAX_SIZE = 100
```

## Types  in datos

```python
# String
name = "Hello World"
name.upper()           # "HELLO WORLD"
name.lower()           # "hello world"
name.replace("H", "J") # "Jello World"

# List (mutable)
numbers = [1, 2, 3, 4, 5]
numbers.append(6)      # [1, 2, 3, 4, 5, 6]
numbers.pop()          # [1, 2, 3, 4, 5]

# Tuple (inmutable)
coords = (10, 20)
x, y = coords

# Set (únicos)
fruits = {"apple", "banana", "orange"}
fruits.add("mango")

# Dictionary
person = {"name": "John", "age": 30}
person["email"] = "john@email.com"
```

## Operadores

```python
# Aritméticos
+, -, *, /, //, %, **

# Comparación
==, !=, <, >, <=, >=

# Lógicos
and, or, not

# Pertenencia
"a" in "apple"        # True
5 in [1, 2, 3, 4, 5]  # True
```

## Control  in flujo

```python
# If-elif-else
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")

# For loop
for i in range(5):
    print(i)          # 0, 1, 2, 3, 4

for fruit in ["apple", "banana"]:
    print(fruit)

# While loop
count = 0
while count < 5:
    count += 1

# List comprehension
squares = [x**2 for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
```

## Funciones

```python
def greet(name: str, greeting: str = "Hello") -> str:
    """Return a greeting message."""
    return f"{greeting}, {name}!"

# Lambda
square = lambda x: x ** 2

# Args y kwargs
def func(*args, **kwargs):
    print(args)    # tuple
    print(kwargs)  # dict
```
