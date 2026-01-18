---
name: basics
description: Quarkus basics and best practices
---

# Quarkus Basics

## Configuración Básica

```properties
# application.properties
quarkus.http.port=8080
quarkus.datasource.jdbc.url=jdbc:postgresql://localhost:5432/mydb
quarkus.datasource.db-kind=postgresql
quarkus.hibernate-orm.database.generation=update
```

## REST Endpoint

```java
import jakarta.ws.rs.*;
import jakarta.ws.rs.core.MediaType;

@Path("/api/hello")
@Produces(MediaType.APPLICATION_JSON)
@Consumes(MediaType.APPLICATION_JSON)
public class HelloResource {

    @GET
    public String hello() {
        return "Hello from Quarkus!";
    }
}
```

## Inyección de Dependencias

```java
import jakarta.inject.Inject;
import org.eclipse.microprofile.inject.Produces;

public class MyService {
    public String process(String input) {
        return input.toUpperCase();
    }
}

@ApplicationScoped
public class ServiceFactory {
    @Produces
    @Inject
    MyService myService;
}
```

## Comandos de Desarrollo

```bash
# Desarrollo con hot-reload
./mvnw quarkus:dev

# Compilar producción
./mvnw package -Dquarkus.package.type=uber-jar

# Construir imagen nativa
./mvnw package -Pnative
```
