---
name: virtual-threads
description: >
  Virtual threads in Java (Project Loom).
  Trigger: When working with Java virtual threads - lightweight threads, structured concurrency, Project Loom
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Java Virtual Threads / Loom"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Java Virtual threads (Java 21+)

## Crear Virtual threads

```java
// Con Thread.ofVirtual()
Thread virtualThread = Thread.ofVirtual().start(() -> {
    System.out.println("Virtual thread: " + Thread.currentThread().getName());
});

// Con factory
ThreadFactory factory = Thread.ofVirtual().factory();

ExecutorService executor = Executors.newVirtualThreadPerTask();

// Builder pattern
Thread vt = Thread.ofVirtual()
    .name("my-vt-")
    .start(() -> {
        System.out.println("Running in virtual thread");
    });
```

## Características

```java
// Los VT son ligeros (millones posibles)
for (int i = 0; i < 1_000_000; i++) {
    int id = i;
    try (var executor = Executors.newVirtualThreadPerTask()) {
        executor.submit(() -> {
            System.out.println("Task " + id);
        });
    }
}

// No pooling necesario
try (var executor = Executors.newVirtualThreadPerTask()) {
    Future<String> future = executor.submit(() -> "Result");
    String result = future.get();
}

// Estructura similar a threads normales
Thread.startVirtualThread(() -> {
    System.out.println("VT running");
});
```

## Virtual threads vs Platform Threads

| Aspect | Platform Thread | Virtual Thread |
|--------|-----------------|----------------|
| Peso | Heavyweight (~1MB) | Lightweight (~1KB) |
| Creación | Costosa | Barata |
| Scheduling | OS | JVM |
| Pooling | Necesario | NO necesario |
| Threads max | Pocos miles | Millones |

## Uso con ExecutorService

```java
// ✅ CORRECTO: No pool
try (var executor = Executors.newVirtualThreadPerTask()) {
    List<Future<String>> futures = new ArrayList<>();
    for (int i = 0; i < 1000; i++) {
        final int taskId = i;
        futures.add(executor.submit(() -> "Task " + taskId));
    }
    // Procesar resultados
}

// ❌ INCORRECTO: No pooling
ExecutorService fixedPool = Executors.newFixedThreadPool(100);  // Mal con VT
```

## Structured Concurrency (Java 21)

```java
import jdk.internal.vm.annotation.Contended;

try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
    var future1 = scope.fork(() -> findUser(1));
    var future2 = scope.fork(() -> findOrder(1));
    
    scope.join();  // Espera todos
    scope.throwIfFailed();
    
    return new UserOrder(future1.resultNow(), future2.resultNow());
}

// ShutdownOnSuccess - termina al primer éxito
try (var scope = new StructuredTaskScope.ShutdownOnSuccess<String>()) {
    scope.fork(() -> searchDB("query"));
    scope.fork(() -> searchCache("query"));
    scope.fork(() -> searchAPI("query"));
    
    return scope.join().resultNow();  // Retorna primer resultado
}
```

## Best Practices

```java
// ✅ Usar con operaciones I/O
try (var executor = Executors.newVirtualThreadPerTask()) {
    List<String> urls = List.of("url1", "url2", "url3");
    List<Future<String>> futures = new ArrayList<>();
    
    for (String url : urls) {
        futures.add(executor.submit(() -> fetchUrl(url)));
    }
    
    return futures.stream()
        .map(future -> {
            try { return future.get(); }
            catch (Exception e) { return "Error"; }
        })
        .toList();
}

// ❌ Evitar sincronización bloqueante en VT
// Los VT se bloquean pero no ocupan threads
synchronized(lock) {
    // OK con VT - otro VT puede continuar
}
```
