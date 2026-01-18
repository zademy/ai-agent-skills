---
name: configuration
description: Configuration in Spring Boot
---

# Configuración Spring Boot

## application.yml

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/mydb
    username: ${DB_USER}
    password: ${DB_PASSWORD}
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true

server:
  port: ${PORT:8080}
  servlet:
    context-path: /api
```

## Configuration Properties

```java
@Configuration
@ConfigurationProperties(prefix = "app")
@Data
public class AppProperties {
    private String name = "MyApp";
    private Database database = new Database();
    
    @Data
    public static class Database {
        private String host = "localhost";
        private int port = 5432;
    }
}
```

## Perfiles

```yaml
# application-dev.yml
spring:
  datasource:
    url: jdbc:h2:mem:devdb

# application-prod.yml
spring:
  datasource:
    url: jdbc:postgresql://prod-server:5432/proddb
```
