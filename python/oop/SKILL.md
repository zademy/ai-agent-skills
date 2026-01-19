---
name: oop
description: >
  Object-oriented programming in Python.
  Trigger: When working with OOP in Python - classes, inheritance, properties, dataclasses, abstract classes
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Python OOP / Classes"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Python OOP

## Clases

```python
class Dog:
    # Class attribute
    species = "Canis familiaris"
    
    def __init__(self, name: str, age: int):
        # Instance attributes
        self.name = name
        self.age = age
    
    def bark(self) -> str:
        return f"{self.name} says Woof!"
    
    def __str__(self) -> str:
        return f"{self.name} is {self.age} years old"

# Usage
dog = Dog("Rex", 3)
print(dog.bark())
print(dog)
```

## Herencia

```python
class Animal:
    def __init__(self, name: str):
        self.name = name
    
    def speak(self) -> str:
        raise NotImplementedError

class Dog(Animal):
    def speak(self) -> str:
        return f"{self.name} barks"

class Cat(Animal):
    def speak(self) -> str:
        return f"{self.name} meows"

# Polymorphism
animals = [Dog("Rex"), Cat("Whiskers")]
for animal in animals:
    print(animal.speak())
```

## Herencia Múltiple y MRO

```python
class A:
    def method(self):
        return "A"

class B:
    def method(self):
        return "B"

class C(A, B):
    pass

c = C()
print(c.method())  # "A" - MRO determines order

# Check MRO
print(C.mro())  # [<class 'C'>, <class 'A'>, <class 'B'>, <class 'object'>]
```

## Properties (Getters/Setters)

```python
class Circle:
    def __init__(self, radius: float):
        self._radius = radius
    
    @property
    def radius(self) -> float:
        return self._radius
    
    @radius.setter
    def radius(self, value: float):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value
    
    @property
    def diameter(self) -> float:
        return self._radius * 2

circle = Circle(5)
print(circle.diameter)  # 10
circle.radius = 10
```

## Classes Abstractas

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass
    
    @abstractmethod
    def perimeter(self) -> float:
        pass

class Rectangle(Shape):
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height
    
    def area(self) -> float:
        return self.width * self.height
    
    def perimeter(self) -> float:
        return 2 * (self.width + self.height)
```

## Dataclasses

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    email: str
    age: int = 0
    
    def __post_init__(self):
        if self.age < 0:
            self.age = 0

user = User("John", "john@email.com", 30)
```

## Mixins

```python
class JSONMixin:
    def to_json(self) -> str:
        import json
        return json.dumps(self.__dict__)

class SerializableMixin:
    def save(self, filename: str):
        with open(filename, 'w') as f:
            f.write(self.to_json())

class User(JSONMixin, SerializableMixin):
    def __init__(self, name: str):
        self.name = name
```
