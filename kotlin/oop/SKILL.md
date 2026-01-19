---
name: oop
description: >
  Object-oriented programming in Kotlin.
  Trigger: When working with Kotlin OOP - classes, inheritance, interfaces, data classes, sealed classes
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Kotlin OOP"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Kotlin OOP

## Clases

```kotlin
// Data class
data class User(
    val id: Int,
    val name: String,
    val email: String
)

// Regular class
class Person(val name: String, var age: Int) {
    // Property con backing field
    var isAdult: Boolean
        get() = age >= 18
        set(value) {
            if (value) age = 18
        }
    
    // Método
    fun greet(): String = "Hello, $name!"
    
    // Secondary constructor
    constructor(name: String) : this(name, 0)
}

// Inheritance
open class Animal(val name: String) {
    open fun speak() = "Some sound"
}

class Dog(name: String) : Animal(name) {
    override fun speak() = "$name barks"
}
```

## Herencia

```kotlin
open class Shape {
    open fun area(): Double = 0.0
}

class Circle(val radius: Double) : Shape() {
    override fun area() = Math.PI * radius * radius
}

class Rectangle(val width: Double, val height: Double) : Shape() {
    override fun area() = width * height
}

// Polimorfismo
val shapes: List<Shape> = listOf(Circle(5.0), Rectangle(4.0, 6.0))
println(shapes.sumOf { it.area() })
```

## Interfaces

```kotlin
interface Drawable {
    fun draw()
    fun getColor(): String
}

interface Clickable {
    fun onClick()
}

class Button(
    val text: String,
    private val color: String = "blue"
) : Drawable, Clickable {
    override fun draw() = println("Drawing $color button: $text")
    override fun onClick() = println("Button clicked!")
}
```

## Abstract Classes

```kotlin
abstract class Vehicle(val brand: String) {
    abstract fun start()
    abstract fun stop()
    
    fun honk() = println("Honk!")
}

class Car(brand: String) : Vehicle(brand) {
    override fun start() = println("$brand car started")
    override fun stop() = println("$brand car stopped")
}
```

## Data Classes

```kotlin
data class Product(
    val id: Int,
    val name: String,
    val price: Double
)

// Auto-generated:
fun main() {
    val p1 = Product(1, "Laptop", 999.99)
    val p2 = Product(1, "Laptop", 999.99)
    
    println(p1 == p2)              // true (equals)
    println(p1.copy())             // copy
    println(p1.copy(price = 899.0)) // copy with modification
    println(listOf(p1).component1()) // componentN
}
```

## Enum Classes

```kotlin
enum class Status(val message: String) {
    PENDING("Pending review"),
    APPROVED("Approved"),
    REJECTED("Rejected");
    
    fun isActive(): Boolean = this != REJECTED
}

val status = Status.APPROVED
println(status.message)       // "Approved"
println(status.name)          // "APPROVED"
println(Status.valueOf("PENDING")) // PENDING
```

## Sealed Classes

```kotlin
sealed class Result<out T> {
    data class Success<T>(val data: T) : Result<T>()
    data class Error(val message: String) : Result<Nothing>()
    object Loading : Result<Nothing>()
}

fun handleResult(result: Result<String>) {
    when (result) {
        is Result.Success -> println(result.data)
        is Result.Error -> println(result.message)
        is Result.Loading -> println("Loading...")
    }
}
```

## Companion Objects

```kotlin
class Config private constructor() {
    companion object {
        private var instance: Config? = null
        
        fun getInstance(): Config {
            if (instance == null) {
                instance = Config()
            }
            return instance!!
        }
    }
}

// Uso
val config = Config.getInstance()
```

## Extension Properties

```kotlin
val String.isPalindrome: Boolean
    get() = this == this.reversed()

val Int.isEven: Boolean
    get() = this % 2 == 0

// Uso
println("radar".isPalindrome)  // true
println(4.isEven)              // true
```

## Delegation

```kotlin
interface Base {
    fun print()
}

class BaseImpl : Base {
    override fun print() = println("Base")
}

class Derived(b: Base) : Base by b

fun main() {
    val b = BaseImpl()
    val d = Derived(b)
    d.print()  // "Base"
}
```
