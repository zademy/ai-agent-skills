---
name: oop
description: Object-oriented programming in PHP
---

# PHP OOP

## Clases

```php
<?php
class User {
    // Constantes
    const ACTIVE = 1;
    const INACTIVE = 0;
    
    // Propiedades
    public string $name;
    public string $email;
    protected int $status;
    private string $password;
    
    // Constructor (PHP 8+)
    public function __construct(
        string $name,
        string $email,
        protected ?int $id = null
    ) {
        $this->name = $name;
        $this->email = $email;
        $this->status = self::ACTIVE;
    }
    
    // Métodos
    public function getName(): string {
        return $this->name;
    }
    
    public function setPassword(string $password): void {
        $this->password = password_hash($password, PASSWORD_DEFAULT);
    }
    
    // Property promotion (PHP 8+)
    public function getEmail(): string {
        return $this->email;
    }
}

$user = new User("John", "john@email.com", 1);
```

## Herencia

```php
class Animal {
    protected string $name;
    
    public function __construct(string $name) {
        $this->name = $name;
    }
    
    public function speak(): string {
        return "Some sound";
    }
}

class Dog extends Animal {
    public function speak(): string {
        return "$this->name barks";
    }
}

$dog = new Dog("Rex");
echo $dog->speak();  // "Rex barks"
```

## Interfaces

```php
interface Drawable {
    public function draw(): void;
    public function getColor(): string;
}

class Circle implements Drawable {
    public function draw(): void {
        echo "Drawing circle";
    }
    
    public function getColor(): string {
        return "red";
    }
}
```

## Abstract Classes

```php
abstract class Shape {
    abstract public function area(): float;
    abstract public function perimeter(): float;
}

class Rectangle extends Shape {
    public function __construct(
        private float $width,
        private float $height
    ) {}
    
    public function area(): float {
        return $this->width * $this->height;
    }
    
    public function perimeter(): float {
        return 2 * ($this->width + $this->height);
    }
}
```

## Traits

```php
trait Loggable {
    public function log(string $message): void {
        echo "[LOG] $message\n";
    }
}

class UserService {
    use Loggable;
    
    public function createUser(array $data): void {
        $this->log("Creating user: " . $data['name']);
        // ...
    }
}
```

## Enum (PHP 8.1+)

```php
enum Status: string {
    case Pending = 'pending';
    case Active = 'active';
    case Inactive = 'inactive';
}

function setStatus(Status $status): void {
    echo $status->value;
}

setStatus(Status::Active);
```

## Magic Methods

```php
class Product {
    private array $data = [];
    
    public function __get(string $name): mixed {
        return $this->data[$name] ?? null;
    }
    
    public function __set(string $name, mixed $value): void {
        $this->data[$name] = $value;
    }
    
    public function __call(string $name, array $args): mixed {
        if (str_starts_with($name, 'get')) {
            $property = strtolower(substr($name, 3));
            return $this->$property;
        }
    }
    
    public function __toString(): string {
        return json_encode($this->data);
    }
}
```

## Constructor Property Promotion

```php
class User {
    public function __construct(
        public string $name,
        public string $email,
        protected ?int $id = null,
        private string $password = ''
    ) {}
}

$user = new User(
    name: "John",
    email: "john@email.com"
);
echo $user->name;  // "John"
```
