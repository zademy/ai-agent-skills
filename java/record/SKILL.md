---
name: record
description: >
  Records in Java (Java 16+).
  Trigger: When working with Java records - immutable data classes, DTOs, validation
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Java Records / Data Classes"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Java Record

## Basic Record

```java
public record User(String name, String email, int age) {
    // Auto-genera:
    // - Campos finales privados
    // - Constructor canónico
    // - Getters (name(), email(), age())
    // - equals(), hashCode(), toString()
}

// Uso
User user = new User("John", "john@email.com", 30);
String name = user.name();
System.out.println(user);
```

## Record con validaciones

```java
public record User(String name, String email) {
    public User {
        Objects.requireNonNull(name, "Name required");
        if (email == null || !email.contains("@")) {
            throw new IllegalArgumentException("Invalid email");
        }
        // Reasignar para normalizar
        email = email.toLowerCase();
    }
}
```

## Record con métodos adicionales

```java
public record Point(int x, int y) {
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
    
    public Point translate(int dx, int dy) {
        return new Point(x + dx, y + dy);
    }
}
```

## Record anidado con static

```java
public record Circle(Point center, double radius) {
    public record Point(int x, int y) {}
}
```

## Record vs Class

| Aspect | Record | Class |
|--------|--------|-------|
| Boilerplate | Mínimo | Manual |
| Mutabilidad | Inmutable | Mutable |
| Uso ideal | DTOs, datos | Entidades complejas |
