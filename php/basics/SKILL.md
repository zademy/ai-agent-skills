---
name: basics
description: PHP basics
---

# PHP Basics

## Variables y Tipos

```php
<?php
// Variables
$name = "John";      // string
$age = 30;           // int
$price = 19.99;      // float
$isActive = true;    // bool

// Constantes
define("PI", 3.14159);
const MAX_SIZE = 100;

// Types de dato
$numbers = [1, 2, 3, 4, 5];
$assoc = ["name" => "John", "age" => 30];

// Objetos
class User {
    public $name;
    public $email;
}
$user = new User();
$user->name = "John";
```

## Operadores

```php
// Aritméticos: +, -, *, /, %, **

// Comparación
==, !=, <, >, <=, >=, ===, !==

// Spaceship
$result = 5 <=> 3;  // 1 (5 > 3)
$result = 3 <=> 5;  // -1 (3 < 5)
$result = 3 <=> 3;  // 0 (equal)

// Null coalescing
$name = $user->name ?? "Anonymous";

// Ternario
$status = $age >= 18 ? "Adult" : "Minor";

// Elvis
$name = $user->name ?: "Default";

// Nullsafe (?->)
echo $user?->getName()?->first();
```

## Control  in flujo

```php
// If
if ($age >= 18) {
    echo "Adult";
} elseif ($age >= 13) {
    echo "Teenager";
} else {
    echo "Child";
}

// Switch
switch ($status) {
    case 'pending':
        echo "Pending";
        break;
    case 'active':
        echo "Active";
        break;
    default:
        echo "Unknown";
}

// Match (PHP 8+)
$result = match($status) {
    'pending' => 'Pending',
    'active' => 'Active',
    default => 'Unknown'
};

// For
for ($i = 0; $i < 5; $i++) {
    echo $i;
}

// Foreach
foreach ($numbers as $num) {
    echo $num;
}

foreach ($assoc as $key => $value) {
    echo "$key: $value";
}

// While
$i = 0;
while ($i < 5) {
    echo $i++;
}

// Do-while
do {
    $i++;
} while ($i < 10);
```

## Funciones

```php
function greet(string $name, string $greeting = "Hello"): string {
    return "$greeting, $name!";
}

// Types nullable
function findUser(?int $id): ?User {
    return $id ? new User() : null;
}

// Union types (PHP 8+)
function process(int|float $number): int|float {
    return $number * 2;
}

// Named arguments
greet(name: "John", greeting: "Hi");

// Variadic
function sum(int ...$numbers): int {
    return array_sum($numbers);
}

// Arrow functions
$numbers = [1, 2, 3, 4, 5];
$squares = array_map(fn($x) => $x ** 2, $numbers);
```
