---
name: lambdas
description: >
  Lambdas and Functional Interfaces in Java.
  Trigger: When working with Java lambdas - lambda expressions, functional interfaces, method references
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Java Lambdas / Functional"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Java Lambdas y Functional Interfaces

## Sintaxis Lambda

```java
// (parameters) -> expression
() -> 42
x -> x * 2
(x, y) -> x + y

// (parameters) -> { statements }
(int x, int y) -> {
    int result = x + y;
    return result;
}
```

## Functional Interfaces Comunes

```java
// Predicate<T> - retorna boolean
Predicate<String> isEmpty = s -> s.isEmpty();
Predicate<Integer> isEven = n -> n % 2 == 0;
List<Integer> numbers = List.of(1, 2, 3, 4, 5);
numbers.stream().filter(isEven).toList();  // [2, 4]

// Function<T, R> - transforma
Function<String, Integer> length = s -> s.length();
Function<Integer, String> stringify = n -> "Number: " + n;
Function<String, String> upper = String::toUpperCase;

// Consumer<T> - consume sin retornar
Consumer<String> printer = s -> System.out.println(s);
Consumer<Integer> doubler = n -> System.out.println(n * 2);
List<String> names = List.of("John", "Jane");
names.forEach(printer);

// Supplier<T> - provee valor
Supplier<Double> random = () -> Math.random();
Supplier<String> greeting = () -> "Hello!";
String value = greeting.get();

// UnaryOperator<T> - T -> T
UnaryOperator<Integer> square = x -> x * x;
UnaryOperator<String> upper = String::toUpperCase;

// BinaryOperator<T> - (T, T) -> T
BinaryOperator<Integer> add = (a, b) -> a + b;
BinaryOperator<Integer> max = Integer::max;
Integer result = max.apply(5, 10);  // 10
```

## Method References

```java
// Static method
Function<Double, Long> round = Math::round;

// Instance method of object
String str = "Hello";
Supplier<Integer> len = str::length;

// Instance method of parameter
Function<String, String> upper = String::toUpperCase;

// Constructor
Supplier<ArrayList<String>> listFactory = ArrayList::new;
List<String> list = listFactory.get();
```

## Built-in Functional Interfaces

```java
// BiPredicate<T, U>
BiPredicate<String, String> equals = String::equals;
BiPredicate<Integer, Integer> greater = (a, b) -> a > b;

// BiFunction<T, U, R>
BiFunction<String, Integer, String> repeat = (s, n) -> s.repeat(n);
String result = repeat.apply("hi", 3);  // "hihihi"

// BiConsumer<T, U>
BiConsumer<String, Integer> print = (s, n) -> System.out.println(s + n);
print.accept("Count: ", 5);  // "Count: 5"

// ToIntFunction, ToLongFunction, ToDoubleFunction
ToIntFunction<String> toInt = s -> s.length();
int len = toInt.applyAsInt("hello");  // 5
```

## Lambdas con Colecciones

```java
List<String> names = List.of("John", "Jane", "Bob", "Alice");

// forEach
names.forEach(name -> System.out.println(name));

// Comparator
names.sort((a, b) -> b.length() - a.length());
names.sort(Comparator.comparing(String::length).reversed());

// Map
List<Integer> lengths = names.stream()
    .map(String::length)
    .toList();

// Filter
List<String> longNames = names.stream()
    .filter(name -> name.length() > 3)
    .toList();
```

## Custom Functional Interface

```java
@FunctionalInterface
interface Operation {
    int apply(int a, int b);
    
    // Static method
    static Operation add() {
        return (a, b) -> a + b;
    }
    
    // Default method
    default void printOp() {
        System.out.println("Operation");
    }
}

// Uso
Operation op = (a, b) -> a * b;
int result = op.apply(3, 4);  // 12
```

## Closure

```java
public class LambdaScope {
    public static void main(String[] args) {
        int number = 10;
        
        // Lambda captura variable externa
        Runnable r = () -> System.out.println(number);
        
        // ❌ No puede modificar variable local
        // number = 20;  // Error de compilación
        
        // Pero sí puede modificar objetos mutables
        int[] counter = {0};
        Runnable increment = () -> counter[0]++;
    }
}
```
