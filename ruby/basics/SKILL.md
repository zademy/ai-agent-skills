---
name: basics
description: Ruby basics
---

# Ruby Basics

## Variables

```ruby
# Variables locales
name = "John"
age = 30

# Constantes (mayúsculas)
PI = 3.14159
MAX_SIZE = 100

# Variables de instancia
@name = "John"

# Variables de clase
@@counter = 0

# Variables globales
$debug = true
```

## Types  in datos

```ruby
# String
name = "Hello World"
name.upcase    # "HELLO WORLD"
name[0]        # "H"

# Integer y Float
integer = 42
float = 3.14

# Array
fruits = ["apple", "banana", "orange"]
fruits << "grape"          # Añadir
fruits[0]                  # "apple"
fruits.first               # "apple"
fruits.last                # "grape"

# Hash (diccionario)
person = { "name" => "John", "age" => 30 }
person[:name]              # "John"
person[:age] = 31          # Modificar

# Symbol
status = :active
```

## Operadores

```ruby
# Aritméticos: +, -, *, /, %, **

# Comparación: ==, !=, <, >, <=, >=, <=>, ===, eql?

# Lógicos: and, or, not

# Ternario
age >= 18 ? "Adult" : "Minor"

# Splat
def greet(*names)
  names.each { |name| puts "Hello, #{name}!" }
end

greet("John", "Jane")  # Hola John, Hola Jane
```

## Control  in flujo

```ruby
# If elsif else
if age >= 18
  "Adult"
elsif age >= 13
  "Teenager"
else
  "Child"
end

# Unless (if negated)
puts "Error" unless valid?

# Case
case status
when :pending then "Pending"
when :active  then "Active"
else "Unknown"
end

# While
i = 0
while i < 5
  puts i
  i += 1
end

# For
for i in 0...5
  puts i
end

# Iterators
(1..5).each do |i|
  puts i
end

# List comprehension (map)
squares = (1..5).map { |i| i ** 2 }  # [1, 4, 9, 16, 25]
```

## Bloques

```ruby
# Block básico
3.times { puts "Hello!" }

# Block con do..end
(1..3).each do |i|
  puts "Number: #{i}"
end

# Block con parámetros
[1, 2, 3].map { |n| n * 2 }  # [2, 4, 6]

# Yield
def greet
  yield "John"
  yield "Jane"
end

greet { |name| puts "Hello, #{name}!" }
```
