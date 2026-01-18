---
name: threads
description: Threads in Java
---

# Java Threads

## Crear Hilos

```java
// Extendiendo Thread
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

MyThread thread = new MyThread();
thread.start();

// Implementando Runnable
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable running");
    }
}

Thread thread = new Thread(new MyRunnable());
thread.start();

// Con lambda
Thread thread = new Thread(() -> {
    System.out.println("Lambda thread");
});
thread.start();
```

## Thread Lifecycle

```
NEW → RUNNABLE → BLOCKED/WAITING → TIMED_WAITING → TERMINATED
```

```java
Thread t = new Thread(() -> {
    for (int i = 0; i < 5; i++) {
        System.out.println(i);
        try {
            Thread.sleep(1000);  // TIMED_WAITING
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
});

t.start();
t.join();  // Espera a que termine
```

## Métodos  in thread

```java
// obtenerThread actual
Thread.currentThread().getName()

// Dormir hilo
Thread.sleep(1000);  // 1 segundo

// Yield
Thread.yield();  // Sugiere al scheduler que pase a otro hilo

// Prioridad (1-10)
thread.setPriority(Thread.MAX_PRIORITY);
thread.setPriority(Thread.MIN_PRIORITY);
thread.setPriority(Thread.NORM_PRIORITY);

// Verificar si está vivo
thread.isAlive();

// Interrumpir
thread.interrupt();
```

## Sincronización

```java
class Counter {
    private int count = 0;
    
    // synchronized method
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}

// Bloque synchronized
class BankAccount {
    private double balance;
    
    public void withdraw(double amount) {
        synchronized (this) {
            if (balance >= amount) {
                balance -= amount;
            }
        }
    }
}

// Lock
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class LockCounter {
    private int count = 0;
    private Lock lock = new ReentrantLock();
    
    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();  // Siempre en finally
        }
    }
}
```

## wait() y notify()

```java
class SharedResource {
    private Queue<String> queue = new LinkedList<>();
    
    public synchronized void produce(String item) {
        queue.add(item);
        notify();  // Notifica a un hilo esperando
    }
    
    public synchronized String consume() throws InterruptedException {
        while (queue.isEmpty()) {
            wait();  // Espera hasta que haya datos
        }
        return queue.poll();
    }
}
```

## ThreadPool

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

// Fixed thread pool
ExecutorService executor = Executors.newFixedThreadPool(4);

executor.execute(() -> {
    System.out.println("Task 1");
});

executor.execute(() -> {
    System.out.println("Task 2");
});

executor.shutdown();

// Callable con Future
ExecutorService executor = Executors.newSingleThreadExecutor();
Future<String> future = executor.submit(() -> {
    return "Result";
});

String result = future.get();  // Bloquea hasta obtener resultado

// Scheduled
ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(2);
scheduler.scheduleAtFixedRate(() -> {
    System.out.println("Every 5 seconds");
}, 0, 5, TimeUnit.SECONDS);
```
