---
name: security
description: Quarkus Security with JWT and OAuth2
---

# Quarkus Security

## JWT Authentication

```properties
# application.properties
quarkus.http.auth.permission.authenticated.paths=/*
quarkus.http.auth.permission.authenticated.policy=authenticated

mp.jwt.verify.publickey.location=publicKey.pem
mp.jwt.verify.issuer=https://auth.empresa.com
```

## Security Identity

```java
import jakarta.annotation.security.RolesAllowed;
import jakarta.inject.Inject;
import io.quarkus.security.identity.SecurityIdentity;

@Path("/api/admin")
public class AdminResource {

    @Inject
    SecurityIdentity identity;

    @GET
    @RolesAllowed({"admin", "manager"})
    public Response adminArea() {
        String username = identity.getPrincipal().getName();
        return Response.ok("Bienvenido admin: " + username).build();
    }
}
```

## JWT Claims

```java
import jakarta.enterprise.context.RequestScoped;
import io.quarkus.security.identity.SecurityIdentity;
import org.eclipse.microprofile.jwt.JsonWebToken;

@RequestScoped
public class UserService {

    @Inject
    JsonWebToken jwt;

    public String getUserEmail() {
        return jwt.getClaim("email");
    }
}
```

## OAuth2 con OIDC

```properties
# application.properties
quarkus.oidc.auth-server-url=https://auth.empresa.com/realms/mi-realm
quarkus.oidc.client-id=mi-app
quarkus.oidc.credentials.secret=mi-secreto
```
