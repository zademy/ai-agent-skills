---
name: class
description: >
  Classes in Java with best practices.
  Trigger: When working with Java classes - constructors, getters/setters, records, Lombok
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Java Classes / OOP"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Classes Java

## Clase Básica

```java
public class User {
    private Long id;
    private String name;
    private String email;
    
    public User() {}
    
    public User(Long id, String name, String email) {
        this.id = id;
        this.name = name;
        this.email = email;
    }
    
    // Getters y Setters
    public Long getId() { return id; }
    public void setId(Long id) { this.id = id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
}
```

## Con Lombok

```java
@Data
@RequiredArgsConstructor
public class User {
    private Long id;
    private String name;
    private String email;
}
```

## Record (Java 14+)

```java
public record UserDTO(Long id, String name, String email) {
    public UserDTO {
        if (id == null || id <= 0) {
            throw new IllegalArgumentException("ID inválido");
        }
    }
}
```
