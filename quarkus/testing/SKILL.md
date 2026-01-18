---
name: testing
description: Quarkus testing with JUnit and Panache
---

# Quarkus Testing

## Test Básico

```java
import io.quarkus.test.junit.QuarkusTest;
import org.junit.jupiter.api.Test;

@QuarkusTest
public class UsuarioResourceTest {

    @Test
    public void testListarUsuarios() {
        given()
            .when().get("/api/usuarios")
            .then()
            .statusCode(200);
    }

    @Test
    public void testCrearUsuario() {
        Usuario usuario = new Usuario("Test", "test@test.com");
        given()
            .contentType(ContentType.JSON)
            .body(usuario)
            .when().post("/api/usuarios")
            .then()
            .statusCode(201);
    }
}
```

## Test con Mock

```java
@QuarkusTest
public class UsuarioServiceTest {

    @InjectMock
    UsuarioRepository usuarioRepository;

    @Test
    public void testBuscarPorId() {
        Mockito.when(usuarioRepository.findById(1L))
            .thenReturn(new Usuario("Test", "test@test.com"));

        given()
            .when().get("/api/usuarios/1")
            .then()
            .statusCode(200);
    }
}
```
