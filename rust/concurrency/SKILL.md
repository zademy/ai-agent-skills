---
name: concurrency
description: Concurrency in Rust
---

# Rust Concurrency

## Threads

```rust
use std::thread;
use std::time::Duration;

fn main() {
    // Crear thread
    let handle = thread::spawn(|| {
        for i in 1..=5 {
            println!("Thread: {}", i);
            thread::sleep(Duration::from_millis(100));
        }
    });
    
    // Main thread
    for i in 1..=3 {
        println!("Main: {}", i);
        thread::sleep(Duration::from_millis(100));
    }
    
    // Esperar a que termine el thread
    handle.join().unwrap();
}
```

## Move Closures

```rust
let v = vec![1, 2, 3];

let handle = thread::spawn(move || {
    println!("Vector: {:?}", v);
});

handle.join().unwrap();
// v ya no es válido aquí (movido al thread)
```

## Channels

```rust
use std::sync::mpsc;

fn main() {
    let (tx, rx) = mpsc::channel();
    
    let tx1 = tx.clone();
    thread::spawn(move || {
        tx1.send("Hello from thread 1").unwrap();
    });
    
    thread::spawn(move || {
        tx.send("Hello from thread 2").unwrap();
    });
    
    for received in rx {
        println!("Received: {}", received);
    }
}
```

## Mutex

```rust
use std::sync::Mutex;
use std::rc::Rc;

fn main() {
    let counter = Mutex::new(0);
    let mut handles = vec![];
    
    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
        });
        handles.push(handle);
    }
    
    for handle in handles {
        handle.join().unwrap();
    }
    
    println!("Result: {}", *counter.lock().unwrap());
}
```

## Arc (Atomic Reference Count)

```rust
use std::sync::Arc;
use std::thread;

fn main() {
    let v = Arc::new(vec![1, 2, 3]);
    let handles: Vec<_> = (0..3).map(|i| {
        let v = Arc::clone(&v);
        thread::spawn(move || {
            println!("Thread {}: {:?}", i, v);
        })
    }).collect();
    
    for handle in handles {
        handle.join().unwrap();
    }
}
```

## Async/Await con Tokio

```rust
use tokio;

#[tokio::main]
async fn main() {
    async fn fetch_data() -> String {
        // Simular operación async
        tokio::time::sleep(tokio::time::Duration::from_secs(1)).await;
        "Data fetched!".to_string()
    }
    
    // Ejecutar múltiples tareas concurrentemente
    let (a, b) = tokio::join!(
        fetch_data(),
        fetch_data()
    );
    
    println!("{}", a);
    println!("{}", b);
}
```

## Future y Spawn

```rust
use tokio::task;

async fn process_item(id: i32) {
    println!("Processing {}", id);
    task::spawn(async move {
        println!("Task spawned for {}", id);
    });
}
```
