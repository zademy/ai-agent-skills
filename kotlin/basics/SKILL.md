---
name: basics
description: Kotlin basics
---

# Kotlin Basics

## Variables

```kotlin
// val (inmutable)
val name = "John"
val age: Int = 30

// var (mutable)
var count = 0
count = 1

// Constantes compile-time
const val MAX_SIZE = 100

// Lateinit
lateinit var database: Database

// Lazy initialization
val config: Config by lazy {
    loadConfig()
}
```

## Types  in datos

```kotlin
// Primitivos (tipo inferido)
val int: Int = 42
val long: Long = 123L
val float: Float = 3.14f
val double: Double = 3.14159
val boolean: Boolean = true
val char: Char = 'A'
val string: String = "Hello"

// Arrays
val numbers: IntArray = intArrayOf(1, 2, 3)
val list: List<String> = listOf("a", "b", "c")
val mutableList: MutableList<Int> = mutableListOf(1, 2, 3)

// Maps
val map: Map<String, Int> = mapOf("a" to 1, "b" to 2)

// Null safety
var name: String? = null
name?.length      // Safe call
name ?: "default" // Elvis operator
name!!.length     // Non-null assertion
```

## Funciones

```kotlin
// Basic function
fun greet(name: String): String {
    return "Hello, $name!"
}

// Single expression
fun add(a: Int, b: Int) = a + b

// Default parameters
fun greet(name: String, greeting: String = "Hello"): String {
    return "$greeting, $name!"
}

// Named arguments
greet(name = "John", greeting = "Hi")

// Vararg
fun sum(vararg numbers: Int): Int {
    return numbers.sum()
}
sum(1, 2, 3, 4, 5)

// Extension function
fun String.addExclamation(): String {
    return this + "!"
}
"Hello".addExclamation()  // "Hello!"

// Lambda
val square = { x: Int -> x * x }
square(5)  // 25
```

## Control  in flujo

```kotlin
// If como expresión
val max = if (a > b) a else b

// When (switch)
when (x) {
    1 -> println("one")
    2 -> println("two")
    in 3..10 -> println("range")
    else -> println("unknown")
}

val result = when (status) {
    "active" -> 1
    "pending" -> 2
    else -> 0
}

// For loops
for (i in 1..5) println(i)      // 1, 2, 3, 4, 5
for (i in 1 until 5) println(i) // 1, 2, 3, 4
for (i in 5 downTo 1) println(i) // 5, 4, 3, 2, 1
for (i in 0..10 step 2) println(i) // 0, 2, 4, 6, 8, 10

// While
var i = 0
while (i < 5) {
    println(i)
    i++
}

// Do-while
do {
    i--
} while (i > 0)

// Iterating collections
val list = listOf("a", "b", "c")
for ((index, value) in list.withIndex()) {
    println("$index: $value")
}

// Break/continue with label
loop@ for (i in 1..10) {
    for (j in 1..10) {
        if (i * j > 50) break@loop
    }
}
```

## Null Safety

```kotlin
var name: String? = null

// Safe calls
println(name?.length)  // null

// Elvis
val len = name?.length ?: 0

// Let
name?.let {
    println("Name is $it")
}

// Also
name?.also {
    println("Assigned: $it")
}
```
