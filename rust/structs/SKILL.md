---
name: structs
description: Structs and Traits in Rust
---

# Rust Structs y Traits

## Structs

```rust
// Basic struct
struct User {
    name: String,
    email: String,
    age: u32,
    active: bool,
}

let user = User {
    name: String::from("John"),
    email: String::from("john@email.com"),
    age: 30,
    active: true,
};

// Tuple struct
struct Point(i32, i32);
let origin = Point(0, 0);

// Unit struct (sin campos)
struct AlwaysEqual;
```

## Struct Methods

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
    
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
    
    // Associated function (static method)
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}
```

## Enums

```rust
enum Message {
    Quit,                   // Sin datos
    Move { x: i32, y: i32 }, // Struct-like
    Write(String),          // Single value
    ChangeColor(u8, u8, u8), // Multiple values
}

impl Message {
    fn call(&self) {
        match self {
            Message::Quit => println!("Quit"),
            Message::Move { x, y } => println!("Move to ({}, {})", x, y),
            Message::Write(text) => println!("Text: {}", text),
            Message::ChangeColor(r, g, b) => println!("Color: {}, {}, {}", r, g, b),
        }
    }
}
```

## Option Enum

```rust
fn divide(a: i32, b: i32) -> Option<i32> {
    if b == 0 {
        None
    } else {
        Some(a / b)
    }
}

let result = divide(10, 2);  // Some(5)
let result = divide(10, 0);  // None

// Unwrap safely
if let Some(value) = result {
    println!("Result: {}", value);
}
```

## Result Enum

```rust
fn read_file(path: &str) -> Result<String, std::io::Error> {
    std::fs::read_to_string(path)
}

let result = read_file("test.txt");
match result {
    Ok(content) => println!("File: {}", content),
    Err(e) => println!("Error: {}", e),
}
```

## Traits

```rust
// Define trait
trait Summary {
    fn summarize(&self) -> String;
}

// Implement trait
impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.text)
    }
}
```

## Default Trait

```rust
#[derive(Default)]
struct User {
    name: String,
    age: u32,
}

let user = User::default();
```

## Clone y Copy

```rust
#[derive(Clone, Copy)]
struct Point {
    x: i32,
    y: i32,
}

let p1 = Point { x: 5, y: 10 };
let p2 = p1;  // Copy, both valid
```
