---
name: error-handling
description: >
  Error handling in Go.
  Trigger: When handling errors in Go - custom errors, error wrapping, panic, recover
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Go Error Handling"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Go Error Handling

## Basic Error

```go
// Definir error
var (
    ErrNotFound     = errors.New("not found")
    ErrInvalidInput = errors.New("invalid input")
)

// Return error
func findUser(id int) (*User, error) {
    if id <= 0 {
        return nil, ErrInvalidInput
    }
    
    user := &User{ID: id}
    // buscar en DB...
    if notFound {
        return nil, ErrNotFound
    }
    
    return user, nil
}

// Usage
user, err := findUser(1)
if err != nil {
    if errors.Is(err, ErrNotFound) {
        fmt.Println("User not found")
    } else {
        fmt.Printf("Error: %v\n", err)
    }
}
```

## Custom Error Types

```go
type ValidationError struct {
    Field   string
    Message string
}

func (e *ValidationError) Error() string {
    return fmt.Sprintf("%s: %s", e.Field, e.Message)
}

func validateUser(u *User) error {
    if u.Name == "" {
        return &ValidationError{Field: "name", Message: "required"}
    }
    return nil
}

// Check custom error
err := validateUser(&User{})
var validationErr *ValidationError
if errors.As(err, &validationErr) {
    fmt.Printf("Validation failed: %s\n", validationErr.Message)
}
```

## Error Wrapping

```go
import "fmt"

// Wrap error
func getUserData(userID int) ([]byte, error) {
    data, err := fetchFromAPI(userID)
    if err != nil {
        return nil, fmt.Errorf("fetch user %d: %w", userID, err)
    }
    return data, nil
}

// Unwrap and check
err := getUserData(1)
if err != nil {
    fmt.Printf("Original error: %v\n", errors.Unwrap(err))
    
    if errors.Is(err, context.DeadlineExceeded) {
        fmt.Println("API timeout")
    }
}
```

## Panic y Recover

```go
func safeDivide(a, b float64) (float64, error) {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered from panic:", r)
        }
    }()
    
    if b == 0 {
        panic("division by zero")
    }
    
    return a / b, nil
}
```

## Error Variables

```go
// Pre-defined errors
var (
    errFileNotFound = os.ErrNotExist
    errPermission   = os.ErrPermission
    errExist        = os.ErrExist
)

// Check
err := openFile("test.txt")
if errors.Is(err, os.ErrNotExist) {
    fmt.Println("File does not exist")
}
```

## Error Dictionary

```go
type ErrorCode int

const (
    ErrCodeNotFound ErrorCode = iota
    ErrCodeInvalid
    ErrCodeUnauthorized
)

func (c ErrorCode) Error() string {
    return [...]string{
        "resource not found",
        "invalid input",
        "unauthorized",
    }[c]
}
```
