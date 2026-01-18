---
name: interface
description: Interfaces in Java
---

# Interfaces Java

## Interface Basic

```java
public interface UserRepository {
    User findById(Long id);
    List<User> findAll();
    User save(User user);
    void deleteById(Long id);
}
```

## Functional Interface

```java
@FunctionalInterface
public interface Processor<T, R> {
    R process(T input);
    
    default Processor<T, R> andThen(Processor<R, R> after) {
        return t -> after.process(process(t));
    }
}
```

## Default Methods

```java
public interface UserService {
    User findById(Long id);
    
    default List<User> findActive() {
        return findAll().stream()
            .filter(u -> "ACTIVE".equals(u.getStatus()))
            .toList();
    }
}
```
