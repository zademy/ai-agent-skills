---
name: clean-code
description: >
  Clean Code principles and best practices for Java development.
  Trigger: When writing clean Java code - SOLID principles, naming, functions, error handling, testing
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Java Clean Code / Best Practices"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Clean Code en Java

## Principios SOLID

### Single Responsibility Principle (SRP)

Una clase debe tener una única responsabilidad.

```java
// ❌ Incorrecto: Múltiples responsabilidades
class UserService {
    void saveUser(User user) { /* guarda usuario */ }
    void sendEmail(User user) { /* envía email */ }
    void generateReport(User user) { /* genera reporte */ }
}

// ✅ Correcto: Responsabilidad única
class UserService {
    private final UserRepository userRepository;
    
    void saveUser(User user) {
        userRepository.save(user);
    }
}

class EmailService {
    void sendEmail(User user) {
        // lógica de envío de email
    }
}

class ReportService {
    void generateReport(User user) {
        // lógica de generación de reporte
    }
}
```

### Open/Closed Principle (OCP)

Las clases deben estar abiertas para extensión pero cerradas para modificación.

```java
// ✅ Correcto: Abierto para extensión, cerrado para modificación
interface DiscountStrategy {
    BigDecimal calculate(BigDecimal amount);
}

class RegularDiscount implements DiscountStrategy {
    @Override
    public BigDecimal calculate(BigDecimal amount) {
        return amount.multiply(BigDecimal.valueOf(0.10));
    }
}

class PremiumDiscount implements DiscountStrategy {
    @Override
    public BigDecimal calculate(BigDecimal amount) {
        return amount.multiply(BigDecimal.valueOf(0.20));
    }
}

class DiscountCalculator {
    private final DiscountStrategy strategy;
    
    public DiscountCalculator(DiscountStrategy strategy) {
        this.strategy = strategy;
    }
    
    public BigDecimal apply(BigDecimal amount) {
        return strategy.calculate(amount);
    }
}
```

### Liskov Substitution Principle (LSP)

Los objetos de una subclase deben poder sustituirse por objetos de su superclase.

```java
// ✅ Correcto: Sustitución válida
interface Bird {
    void fly();
}

class Sparrow implements Bird {
    @Override
    public void fly() {
        System.out.println(" Sparrow flying");
    }
}

class Penguin implements Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Penguins cannot fly");
    }
}

// ✅ Mejor diseño
interface Bird {}
interface FlyingBird extends Bird { void fly(); }
interface SwimmableBird extends Bird { void swim(); }

class Sparrow implements FlyingBird {
    @Override
    public void fly() { /* ... */ }
}

class Penguin implements SwimmableBird {
    @Override
    public void swim() { /* ... */ }
}
```

### Interface Segregation Principle (ISP)

Es mejor tener muchas interfaces específicas que una interfaz general.

```java
// ❌ Incorrecto: Interfaz demasiado grande
interface Worker {
    void work();
    void eat();
    void sleep();
    void code();
}

// ✅ Correcto: Interfaces segregadas
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

interface Sleepable {
    void sleep();
}

class Developer implements Workable, Eatable, Sleepable {
    @Override
    public void work() { /* código */ }
    
    @Override
    public void eat() { /* come */ }
    
    @Override
    public void sleep() { /* duerme */ }
}

class Robot implements Workable {
    @Override
    public void work() { /* trabaja */ }
}
```

### Dependency Inversion Principle (DIP)

Depender de abstracciones, no de concreciones.

```java
// ✅ Correcto: Dependencia de abstracciones
interface NotificationService {
    void send(String message);
}

class EmailNotification implements NotificationService {
    @Override
    public void send(String message) {
        // envío por email
    }
}

class SMSNotification implements NotificationService {
    @Override
    public void send(String message) {
        // envío por SMS
    }
}

class OrderService {
    private final NotificationService notificationService;
    
    // Inyección de dependencia
    public OrderService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
    
    void processOrder(Order order) {
        // lógica de procesamiento
        notificationService.send("Order processed");
    }
}
```

## Nombres Significativos

### Variables y Métodos

```java
// ❌ Incorrecto
int d; // días?
List list;
void proc() {}

✅ Correcto
int daysSinceLastLogin;
List<User> activeUsers;
void processOrder() {}

// ✅ Nombres que describen intención
BigDecimal calculateTotalPriceIncludingTax();
List<User> findUsersWithActiveSubscription();
Map<String, Product> getProductsByCategory();
```

### Clases y Constants

```java
// ❌ Incorrecto
class Data {}
class Info {}
class Manager {}
final int A = 100;

// ✅ Correcto
class UserRepository {}
class PaymentProcessor {}
final int MAX_RETRY_ATTEMPTS = 3;
final BigDecimal DEFAULT_TAX_RATE = BigDecimal.valueOf(0.16);
```

## Funciones

### Tamaño y Responsabilidad

```java
// ❌ Incorrecto: Función demasiado larga
void processUserRegistration(User user) {
    validateUser(user);
    saveUserToDatabase(user);
    sendWelcomeEmail(user);
    generateUserProfile(user);
    logRegistration(user);
    notifyAdmins(user);
    updateStatistics(user);
    // 50 líneas más...
}

// ✅ Correcto: Funciones pequeñas y enfocadas
void processUserRegistration(User user) {
    validateUser(user);
    User savedUser = saveUser(user);
    sendWelcomeEmail(savedUser);
    createUserProfile(savedUser);
    notifyNewUserRegistration(savedUser);
}

private User saveUser(User user) {
    return userRepository.save(user);
}
```

### Parámetros

```java
// ❌ Demasiados parámetros
User createUser(String name, String email, String phone,
                String address, int age, boolean active) {}

// ✅ Mejor: Objeto parámetro o método dedicado
record UserData(String name, String email, String phone,
                String address, int age) {}

User createUser(UserData userData) {}

// O métodos específicos
User createUserWithNameAndEmail(String name, String email) {}
void updateUserAddress(Long userId, String newAddress) {}
```

### Evitar efectos secundarios

```java
// ❌ Efecto secundario oculto
public boolean login(String username, String password) {
    User user = findUserByUsername(username);
    if (user != null && password.equals(user.getPassword())) {
        Session.create(user); // Efecto secundario
        return true;
    }
    return false;
}

// ✅ Efecto secundario explícito
public Session login(String username, String password) {
    User user = findUserByUsername(username);
    if (user != null && password.equals(user.getPassword())) {
        return Session.create(user);
    }
    throw new AuthenticationFailedException();
}
```

## Comentarios

### Cuándo Usar Comentarios

```java
// ✅ Explicar el "por qué", no el "qué"
/**
 * Calcula el precio total considerando descuentos progresivos
 * según la cantidad de items (mayor cantidad = mayor descuento)
 */
BigDecimal calculateTotalPrice(List<OrderItem> items) {
    // Regla de negocio: 5% adicional por cada 10 items
    BigDecimal baseDiscount = determineBaseDiscount(items);
    return applyProgressiveDiscount(baseDiscount, items);
}

// ✅ Documentar casos edge complejos
/**
 * @param value Valor a validar
 * @return true si el valor está en rango válido [0, 1] o null
 * @throws IllegalArgumentException si el valor está fuera de rango
 */
public boolean isValidPercentage(BigDecimal value) {
    if (value == null) return true;
    return value.compareTo(BigDecimal.ZERO) >= 0
        && value.compareTo(BigDecimal.ONE) <= 0;
}
```

### Evitar Comentarios

```java
// ❌ Comentario que no aporta valor
// Incrementa el contador
counter++;

// ✅ Código auto-explicativo
failedLoginAttempts.increment();

// ❌ Código comentado
// User user = userService.findById(id);
// if (user != null) { ... }

// ✅ Eliminar código muerto
// Usar control de versiones para recuperar código anterior
```

## Formateo y Estilo

### Espaciado y Líneas en Blanco

```java
// ✅ Espaciado consistente
public class UserService {
    
    private final UserRepository userRepository;
    private final EmailService emailService;
    
    public UserService(UserRepository userRepository, EmailService emailService) {
        this.userRepository = userRepository;
        this.emailService = emailService;
    }
    
    public Optional<User> findById(Long id) {
        return userRepository.findById(id);
    }
    
    public void registerNewUser(User user) {
        validateUserData(user);
        User savedUser = userRepository.save(user);
        emailService.sendWelcomeEmail(savedUser);
    }
    
    private void validateUserData(User user) {
        // validación
    }
}
```

### Longitud de Línea

```java
// ✅ Dividir líneas largas
List<User> activeUsers = userRepository.findAll()
    .stream()
    .filter(User::isActive)
    .filter(user -> user.getLastLogin()
        .isAfter(LocalDateTime.now().minusMonths(6)))
    .toList();

// ✅ Métodos con muchos parámetros
User createUser(
        String name,
        String email,
        String phoneNumber,
        String address,
        LocalDate birthDate
) {
    // ...
}
```

## Estándares de Código (Límites Recomendados)

Basado en "Clean Code" de Robert C. Martin, estos son los límites profesionales para asegurar código legible:

| Métrica | Límite Clean Code | Descripción |
|---------|-------------------|-------------|
| Líneas por Clase | < 200 | Evita el "Objeto Dios" (God Object) |
| Líneas por Método | 5 - 15 | Un método debe caber en la pantalla sin hacer scroll |
| Parámetros por Método | Máximo 3 | Facilita las pruebas unitarias y evita confusiones |
| Métodos Privados | Los necesarios | Se usan para descomponer métodos públicos complejos |
| Variables de Instancia | Ideal < 10 | Muchas variables indican demasiadas responsabilidades |
| Anidamiento (Indent) | Máximo 1 - 2 niveles | Evita el "Código Espagueti" |

### Ejemplos de Aplicación

```java
// ✅ Clase dentro del límite (menos de 200 líneas)
class UserValidator {
    
    private final UserRepository userRepository;
    private final EmailService emailService;
    
    public UserValidator(UserRepository userRepository, EmailService emailService) {
        this.userRepository = userRepository;
        this.emailService = emailService;
    }
    
    public ValidationResult validate(User user) {
        if (!isValidEmail(user.getEmail())) {
            return ValidationResult.failure("Invalid email");
        }
        if (!isValidAge(user.getAge())) {
            return ValidationResult.failure("Invalid age");
        }
        if (userRepository.existsByEmail(user.getEmail())) {
            return ValidationResult.failure("Email already exists");
        }
        return ValidationResult.success();
    }
    
    private boolean isValidEmail(String email) {
        return email != null && email.contains("@");
    }
    
    private boolean isValidAge(Integer age) {
        return age != null && age >= 18;
    }
}

// ❌ Clase demasiado larga (viola SRP y límite de líneas)
class GodClass {
    private int a, b, c, d, e, f, g, h, i, j, k;
    private String x, y, z, w, v, u, t, s, r;
    // ... 500+ líneas con múltiples responsabilidades
}
```

## Manejo de Errores

### Excepciones en Lugar de Códigos de Retorno

```java
// ❌ Códigos de retorno
class Result<T> {
    private final T value;
    private final String error;
    
    static <T> Result<T> success(T value) { ... }
    static <T> Result<T> error(String message) { ... }
}

// ✅ Excepciones
class UserNotFoundException extends RuntimeException {
    public UserNotFoundException(Long userId) {
        super("User not found with id: " + userId);
    }
}

class InvalidUserDataException extends RuntimeException {
    public InvalidUserDataException(String message) {
        super(message);
    }
}

public User findUserById(Long id) {
    return userRepository.findById(id)
        .orElseThrow(() -> new UserNotFoundException(id));
}
```

### Excepciones Personalizadas

```java
// ✅ Jerarquía de excepciones
abstract class ApplicationException extends RuntimeException {
    private final ErrorCode errorCode;
    
    protected ApplicationException(String message, ErrorCode errorCode) {
        super(message);
        this.errorCode = errorCode;
    }
    
    public ErrorCode getErrorCode() {
        return errorCode;
    }
}

enum ErrorCode {
    USER_NOT_FOUND,
    INVALID_OPERATION,
    DATA_INTEGRITY_VIOLATION
}

class UserNotFoundException extends ApplicationException {
    public UserNotFoundException(Long userId) {
        super("User not found with id: " + userId, ErrorCode.USER_NOT_FOUND);
    }
}
```

### Try-with-Resources

```java
// ❌ Finally block
Connection conn = null;
try {
    conn = dataSource.getConnection();
    // operaciones
} finally {
    if (conn != null) {
        conn.close();
    }
}

// ✅ Try-with-resources
try (Connection conn = dataSource.getConnection();
     PreparedStatement stmt = conn.prepareStatement(sql)) {
    // operaciones
}
```

## Testing

### Estructura de Tests

```java
class UserServiceTest {
    
    private UserService userService;
    private UserRepository userRepository;
    
    @BeforeEach
    void setUp() {
        userRepository = mock(UserRepository.class);
        userService = new UserService(userRepository);
    }
    
    @Test
    @DisplayName("Should throw exception when user not found")
    void findById_whenUserNotFound_throwsException() {
        // Given
        Long userId = 999L;
        when(userRepository.findById(userId)).thenReturn(Optional.empty());
        
        // When & Then
        assertThrows(UserNotFoundException.class,
            () -> userService.findById(userId));
    }
    
    @Test
    @DisplayName("Should return user when found")
    void findById_whenUserExists_returnsUser() {
        // Given
        Long userId = 1L;
        User expectedUser = new User(userId, "John");
        when(userRepository.findById(userId)).thenReturn(Optional.of(expectedUser));
        
        // When
        User result = userService.findById(userId);
        
        // Then
        assertEquals(expectedUser, result);
    }
}
```

### Buenas Prácticas en Tests

```java
// ✅ Nombres descriptivos
@Test
@DisplayName("Should apply 20% discount for premium customers")
void shouldApplyDiscountForPremiumCustomers() {}

// ✅ Un solo assertion por test (idealmente)
@Test
void shouldCreateUserWithDefaultStatus() {
    User user = userService.createUser("John", "john@email.com");
    
    assertNotNull(user.getId());
    assertEquals("John", user.getName());
    assertEquals(UserStatus.ACTIVE, user.getStatus());
}

// ✅ Tests independientes
@Test
void shouldProcessOrderIndependently() {
    // Este test no depende de otros tests
}
```

## Código Duplicado

### Extracción de Métodos

```java
// ❌ Código duplicado
void processPayment(CreditCard card, BigDecimal amount) {
    if (card.isExpired()) {
        throw new InvalidPaymentException("Card expired");
    }
    // procesar pago
}

void processPayment(DebitCard card, BigDecimal amount) {
    if (card.isExpired()) {
        throw new InvalidPaymentException("Card expired");
    }
    // procesar pago
}

// ✅ Extracción de lógica común
interface PaymentCard {
    boolean isExpired();
}

void validateCard(PaymentCard card) {
    if (card.isExpired()) {
        throw new InvalidPaymentException("Card expired");
    }
}
```

## Referencias

- "Clean Code" por Robert C. Martin
- "Effective Java" por Joshua Bloch
- Principios SOLID
