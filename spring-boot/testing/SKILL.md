---
name: testing
description: Testing in Spring Boot
---

# Spring Boot Testing

## Dependencias

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

## Unit Test con MockMvc

```java
@WebMvcTest(UserController.class)
class UserControllerTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @MockBean
    private UserService userService;
    
    @Test
    void getUser_shouldReturnUser() throws Exception {
        User user = new User(1L, "John", "john@email.com");
        when(userService.findById(1L)).thenReturn(user);
        
        mockMvc.perform(get("/users/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("John"))
            .andExpect(jsonPath("$.email").value("john@email.com"));
    }
    
    @Test
    void createUser_shouldReturn201() throws Exception {
        User user = new User(null, "Jane", "jane@email.com");
        when(userService.save(any(User.class))).thenReturn(user);
        
        mockMvc.perform(post("/users")
            .contentType(MediaType.APPLICATION_JSON)
            .content("""{"name": "Jane", "email": "jane@email.com"}"""))
            .andExpect(status().isCreated());
    }
}
```

## DataJpaTest

```java
@DataJpaTest
class UserRepositoryTest {
    
    @Autowired
    private UserRepository userRepository;
    
    @Test
    void findByEmail_shouldReturnUser() {
        User user = new User("John", "john@email.com");
        userRepository.save(user);
        
        User found = userRepository.findByEmail("john@email.com").orElse(null);
        
        assertThat(found).isNotNull();
        assertThat(found.getName()).isEqualTo("John");
    }
}
```

## Service Test

```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    
    @Mock
    private UserRepository userRepository;
    
    @InjectMocks
    private UserService userService;
    
    @Test
    void save_shouldReturnSavedUser() {
        User user = new User("John", "john@email.com");
        when(userRepository.save(user)).thenReturn(user);
        
        User result = userService.save(user);
        
        assertThat(result).isNotNull();
        assertThat(result.getName()).isEqualTo("John");
        verify(userRepository).save(user);
    }
}
```

## TestContainers

```java
@Testcontainers
@SpringBootTest
class DatabaseTest {
    
    @Container
    static PostgreSQLContainer<?> postgres =
        new PostgreSQLContainer<>("postgres:15")
            .withDatabaseName("test")
            .withUsername("test")
            .withPassword("test");
    
    @DynamicPropertySource
    static void configureProperties(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
    }
}
```
