---
name: interface
description: >
  Interfaces in Java.
  Trigger: When working with Java interfaces - functional interfaces, default methods, abstract methods
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Java Interfaces / Contracts"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
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
