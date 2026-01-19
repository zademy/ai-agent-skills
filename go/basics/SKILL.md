---
name: basics
description: >
  Go basics.
  Trigger: When working with Go - variables, types, control flow, functions, pointers
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Go / Backend"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Go Basics

## Variables y Tipos

```go
// Declaración básica
var name string = "John"
var age int = 30
var isActive bool = true

// Inferencia de tipos
var name = "John"  // string
age := 30          // int (short declaration)

// Múltiples variables
var (
    firstName = "John"
    lastName  = "Doe"
)

// Constantes
const Pi = 3.14159
const (
    StatusOK  = "ok"
    StatusErr = "error"
)
```

## Types  in datos

```go
// Enteros
var i int      // Platform dependent
var i8 int8    // -128 to 127
var i16 int16
var i32 int32
var i64 int64
var u uint     // Unsigned
var u8 uint8
var u16 uint16

// Flotantes
var f32 float32
var f64 float64

// Strings
var s string = "Hello"
s[0]          // Bytes (H)

// Arrays (tamaño fijo)
var arr [5]int           // [0, 0, 0, 0, 0]
arr := [3]int{1, 2, 3}

// Slices (dynamic)
slice := []int{1, 2, 3}
slice = append(slice, 4)
slice = append(slice, 5, 6)

// Maps
m := map[string]int{
    "a": 1,
    "b": 2,
}
m["c"] = 3

// Structs
type Person struct {
    Name string
    Age  int
}
p := Person{Name: "John", Age: 30}
```

## Control  in flujo

```go
// If
if age >= 18 {
    fmt.Println("Adult")
} else if age >= 13 {
    fmt.Println("Teenager")
} else {
    fmt.Println("Child")
}

// For (único loop)
for i := 0; i < 10; i++ {
    fmt.Println(i)
}

// Range
for index, value := range slice {
    fmt.Println(index, value)
}

for key, value := range map {
    fmt.Println(key, value)
}

// While (for sin init/increment)
n := 0
for n < 5 {
    n++
    fmt.Println(n)
}

// Switch
switch day := time.Now().Weekday(); day {
case time.Saturday:
    fmt.Println("Weekend")
case time.Sunday:
    fmt.Println("Weekend")
default:
    fmt.Println("Weekday")
}
```

## Funciones

```go
// Basic
func greet(name string) string {
    return "Hello, " + name
}

// Multiple return
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}

// Named return
func rectangleProps(width, height float64) (area, perimeter float64) {
    area = width * height
    perimeter = 2 * (width + height)
    return // Naked return
}

// Variadic
func sum(nums ...int) int {
    total := 0
    for _, n := range nums {
        total += n
    }
    return total
}
```

## Punteros

```go
func modifyValue(x *int) {
    *x = 42
}

func main() {
    value := 10
    modifyValue(&value)
    fmt.Println(value)  // 42
}
```
