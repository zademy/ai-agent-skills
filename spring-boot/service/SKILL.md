---
name: service
description: Services in Spring Boot
---

# Services Spring Boot

## Service Basic

```java
@Service
@Transactional
@RequiredArgsConstructor
public class UserService {
    
    private final UserRepository userRepository;
    
    public UserDTO findById(Long id) {
        return userRepository.findById(id)
                .map(this::toDTO)
                .orElseThrow(() -> new UserNotFoundException(id));
    }
    
    public List<UserDTO> findAll() {
        return userRepository.findAll().stream()
                .map(this::toDTO)
                .toList();
    }
    
    public UserDTO create(CreateUserRequest request) {
        if (userRepository.existsByEmail(request.email())) {
            throw new BusinessException("Email ya registrado");
        }
        User user = toEntity(request);
        return toDTO(userRepository.save(user));
    }
}
```
