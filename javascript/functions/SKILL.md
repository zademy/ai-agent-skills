---
name: functions
description: >
  Functions in modern JavaScript.
  Trigger: When working with functions - arrow functions, closures, parameters, callbacks
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Functions / Callbacks"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Functions JavaScript

## Arrow Functions

```javascript
const greet = name => `Hola, ${name}`
const add = (a, b) => a + b
const getRandom = () => Math.random()

const process = (value) => {
    const result = value * 2
    return result
}
```

## Parámetros por Defecto

```javascript
function greet(name = 'Usuario') {
    return `Hola, ${name}`
}

function createUser(name, role = 'USER', active = true) {
    return { name, role, active }
}
```

## Rest Parameters

```javascript
function sum(...numbers) {
    return numbers.reduce((a, b) => a + b, 0)
}
```

## Closures

```javascript
function createCounter() {
    let count = 0
    return {
        increment: () => ++count,
        decrement: () => --count,
        getValue: () => count
    }
}
```
