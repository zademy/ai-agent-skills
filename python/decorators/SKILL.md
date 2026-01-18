---
name: decorators
description: Decorators in Python
---

# Python Decorators

## Basic Decorator

```python
def uppercase_decorator(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result.upper()
    return wrapper

@uppercase_decorator
def greet(name):
    return f"Hello, {name}"

print(greet("John"))  # "HELLO, JOHN"
```

## Decorator with Arguments

```python
def repeat(times: int):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def say_hello():
    print("Hello!")

# Calls say_hello() 3 times
```

## Class Decorator

```python
class Timer:
    def __init__(self, func):
        self.func = func
    
    def __call__(self, *args, **kwargs):
        import time
        start = time.time()
        result = self.func(*args, **kwargs)
        end = time.time()
        print(f"{self.func.__name__} took {end-start:.4f}s")
        return result

@Timer
def slow_function():
    import time
    time.sleep(1)

slow_function()
```

## Built-in Decorators

```python
# @staticmethod - método estático
class Math:
    @staticmethod
    def add(a, b):
        return a + b

# @classmethod - método de clase
class Person:
    count = 0
    
    @classmethod
    def create(cls, name):
        cls.count += 1
        return cls(name)

# @property - getter/setter
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def diameter(self):
        return self._radius * 2
```

## functools.wraps

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        """Wrapper function docstring."""
        print("Before call")
        result = func(*args, **kwargs)
        print("After call")
        return result
    return wrapper

@my_decorator
def my_function():
    """My function docstring."""
    pass

print(my_function.__name__)  # "my_function" (not "wrapper")
print(my_function.__doc__)   # "My function docstring."
```

## Multiple Decorators

```python
@decorator1
@decorator2
@decorator3
def my_function():
    pass

# Equivalent to: decorator1(decorator2(decorator3(my_function)))
```

## Decorator for Methods

```python
def require_auth(func):
    @wraps(func)
    def wrapper(self, *args, **kwargs):
        if not hasattr(self, 'is_authenticated'):
            raise PermissionError("Not authenticated")
        if not self.is_authenticated:
            raise PermissionError("Access denied")
        return func(self, *args, **kwargs)
    return wrapper

class Dashboard:
    is_authenticated = True
    
    @require_auth
    def view_data(self):
        return "Secret data"
```
