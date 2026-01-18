---
name: metaprogramming
description: Metaprogramming in Ruby
---

# Ruby Metaprogramming

## Dynamic Methods

```ruby
class Calculator
  [:add, :subtract, :multiply, :divide].each do |method|
    define_method(method) do |a, b|
      a.send(method, b)
    end
  end
end

calc = Calculator.new
puts calc.add(2, 3)        # 5
puts calc.multiply(4, 5)   # 20
```

## method_missing

```ruby
class DynamicLogger
  def method_missing(method_name, *args)
    if method_name.to_s.start_with?("log_")
      level = method_name.to_s.sub("log_", "")
      puts "[#{level.upcase}] #{args.join(', ')}"
    else
      super.method_missing(method_name, *args)
    end
  end
  
  def respond_to_missing?(method_name, include_private = false)
    method_name.to_s.start_with?("log_") || super
  end
end

logger = DynamicLogger.new
logger.log_info("User logged in")    # [INFO] User logged in
logger.log_debug("Data loaded")      # [DEBUG] Data loaded
```

## class_eval y instance_eval

```ruby
# instance_eval - ejecuta en el contexto  of the instancia
class User
  attr_accessor :name, :email
end

user = User.new
user.instance_eval do
  @name = "John"
  @email = "john@email.com"
end

# class_eval - añade métodos de clase
String.class_eval do
  def shout
    upcase + "!"
  end
end

puts "hello".shout    # "HELLO!"
```

## define_method

```ruby
class Person
  attributes = [:name, :email, :age, :city]
  
  attributes.each do |attr|
    define_method(attr) do
      instance_variable_get("@#{attr}")
    end
    
    define_method("#{attr}=") do |value|
      instance_variable_set("@#{attr}", value)
    end
  end
end

person = Person.new
person.name = "John"
person.email = "john@email.com"
puts person.name    # "John"
```

## Modules extend y include

```ruby
module Authenticator
  def authenticate(password)
    password == "secret"
  end
end

class User
  inclu in authenticator
end

user = User.new
puts user.authenticate("secret")   # true

# extend añade métodos de clase
class Admin
  extend Authenticator
end

puts Admin.authenticate("secret")  # true
```

## Eigenclass (Singleton Class)

```ruby
class Dog
  def bark
    "Woof!"
  end
end

dog = Dog.new

# Añadir método solo a esta instancia
class << dog
  def jump
    "Jumping!"
  end
end

puts dog.jump    # "Jumping!"
# Otros dogs no tienen jump

# Leer eigenclass
class Dog
  class << self
    def species
      "Canis familiaris"
    end
  end
end
```

## ActiveSupport-like Extensions

```ruby
# Añadir métodos a clases existentes
class String
  def titleize
    split.map(&:capitalize).join(' ')
  end
end

puts "hello world".titleize    # "Hello World"

class Array
  def sum
    inject(0, :+)
  end
end

puts [1, 2, 3, 4].sum    # 10
```
