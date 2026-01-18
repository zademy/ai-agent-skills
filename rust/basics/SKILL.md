---
name: basics
description: Rust basics
---

# Rust Basics

## Variables y Mutabilidad

```rust
// Inmutable por defecto
let x = 5;
x = 6; // Error!

// Mutable
let mut y = 5;
y = 6; // OK

// Constantes
const MAX_SIZE: u32 = 100;

// Shadowing
let z = 5;
let z = z + 1;  // Nueva variable
let z = z * 2;
```

## Types  in datos

```rust
// Escalares
let integer: i32 = 42;        // Entero con signo
let unsigned: u32 = 100;      // Entero sin signo
let float: f64 = 3.14;        // Flotante
let bool: bool = true;        // Booleano
let letter: char = 'A';       // Caracter

// Compuestos
// Tuple
let tuple: (i32, f64, char) = (500, 6.4, 'z');
let (a, b, c) = tuple;

// Array (tamaño fijo)
let arr = [1, 2, 3, 4, 5];
let first = arr[0];
let arr2: [i32; 5] = [1, 2, 3, 4, 5];
let repeated = [3; 5];  // [3, 3, 3, 3, 3]
```

## Funciones

```rust
fn greet(name: &str) -> String {
    format!("Hello, {}!", name)
}

// Multiple returns
fn swap(a: i32, b: i32) -> (i32, i32) {
    (b, a)
}

// Early return
fn example(x: i32) -> i32 {
    if x > 10 {
        return 99;
    }
    x + 1
}
```

## Control  in flujo

```rust
// If
let number = 6;
if number % 3 == 0 {
    println!("divisible by 3");
} else if number % 2 == 0 {
    println!("divisible by 2");
} else {
    println!("not divisible by 2 or 3");
}

// Let with if
let condition = true;
let value = if condition { 5 } else { 10 };

// Loop
let mut counter = 0;
loop {
    counter += 1;
    if counter == 10 {
        break;
    }
}

// While
while counter > 0 {
    println!("{}", counter);
    counter -= 1;
}

// For
let arr = [10, 20, 30];
for element in arr {
    println!("{}", element);
}

// Range
for i in 1..=5 {
    println!("{}", i);  // 1, 2, 3, 4, 5
}
```

## Ownership

```rust
// Ownership moves
let s1 = String::from("hello");
let s2 = s1;  // s1 ya no es válido

// References (borrowing)
fn calculate_length(s: &String) -> usize {
    s.len()
}

// Mutable references
fn modify_string(s: &mut String) {
    s.push_str(" world");
}
```
