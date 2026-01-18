---
name: enum
description: Enums in Java
---

# Java Enum

## Basic Enum

```java
public enum Direction {
    NORTH, SOUTH, EAST, WEST
}
```

## Enum con campos y métodos

```java
public enum Status {
    PENDING("Pendiente"),
    APPROVED("Aprobado"),
    REJECTED("Rechazado");
    
    private final String spanishName;
    
    Status(String spanishName) {
        this.spanishName = spanishName;
    }
    
    public String getSpanishName() {
        return spanishName;
    }
}
```

## Enum con abstract methods

```java
public enum Operation {
    ADD {
        public int apply(int a, int b) { return a + b; }
    },
    SUBTRACT {
        public int apply(int a, int b) { return a - b; }
    };
    
    public abstract int apply(int a, int b);
}
```

## Enum singleton pattern

```java
public enum Singleton {
    INSTANCE;
    
    public void doSomething() {
        System.out.println("Singleton action");
    }
}
```
