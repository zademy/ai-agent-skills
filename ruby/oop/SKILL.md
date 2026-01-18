---
name: oop
description: Object-oriented programming in Ruby
---

# Ruby OOP

## Clases

```ruby
class Dog
  # Constante de clase
  SPECIES = "Canis familiaris"
  
  # Atributos
  attr_accessor :name, :age  # Getter y Setter
  attr_reader :breed         # Solo Getter
  attr_writer :weight        # Solo Setter
  
  def initialize(name, age, breed)
    @name = name    # Variable de instancia
    @age = age
    @breed = breed
  end
  
  # Método de instancia
  def bark
    "#{@name} says Woof!"
  end
  
  # Método de clase
  def self.species
    SPECIES
  end
  
  # to_s override
  def to_s
    "#{@name} is a #{@age} year old #{@breed}"
  end
end

# Uso
dog = Dog.new("Rex", 3, "Labrador")
puts dog.bark     # "Rex says Woof!"
puts dog.name     # "Rex"
dog.name = "Max"
puts dog
```

## Herencia

```ruby
class Animal
  def initialize(name)
    @name = name
  end
  
  def speak
    raise NotImplementedError
  end
end

class Dog < Animal
  def speak
    "#{@name} barks"
  end
end

class Cat < Animal
  def speak
    "#{@name} meows"
  end
end

# Polimorfismo
animals = [Dog.new("Rex"), Cat.new("Whiskers")]
animals.each { |animal| puts animal.speak }
```

## Módulos (Mixins)

```ruby
module Walkable
  def walk
    "#{@name} is walking"
  end
end

module Swimmable
  def swim
    "#{@name} is swimming"
  end
end

class Duck < Animal
  inclu in walkable
  inclu in swimmable
end

duck = Duck.new("Donald")
puts duck.walk    # "Donald is walking"
puts duck.swim    # "Donald is swimming"
```

## Módulos como Namespaces

```ruby
module Services
  class UserService
    def self.create_user(name)
      User.new(name)
    end
  end
  
  class PaymentService
    def process(payment)
      # ...
    end
  end
end

Services::UserService.create_user("John")
```

## Singleton Methods

```ruby
class Dog
  def bark
    "Woof!"
  end
end

dog = Dog.new
def dog.special_trick
  "Playing dead"
end

puts dog.bark           # "Woof!"
puts dog.special_trick  # "Playing dead"
# Otros dogs no tienen special_trick
```

## Duck Typing

```ruby
class Duck
  def quack
    "Quack!"
  end
end

class Person
  def quack
    "I'm quacking like a duck!"
  end
end

def make_it_quack(duck)
  puts duck.quack
end

make_it_quack(Duck.new)     # "Quack!"
make_it_quack(Person.new)   # "I'm quacking like a duck!"
```

## Private y Protected

```ruby
class BankAccount
  def initialize(balance)
    @balance = balance
  end
  
  # Private (no puede acceder con receptor)
  private
  
  def validate_amount(amount)
    amount > 0
  end
  
  # Protected (puede acceder con self o otro objeto  of the misma clase)
  protected
  
  def compare_balance(other)
    @balance <=> other.@balance
  end
end
```

## Alias Method

```ruby
class Array
  alias_method :old_size, :size
  
  def size
    puts "Size called!"
    old_size
  end
end
```
