---
name: interfaces
description: Interfaces in TypeScript
---

# Interfaces TypeScript

## Interface Básica

```typescript
interface User {
  id: number
  name: string
  email: string
  age?: number  // Opcional
  readonly createdAt: Date  // Solo lectura
}
```

## Herencia  in interfaces

```typescript
interface Animal {
  name: string
}

interface Dog extends Animal {
  breed: string
  bark(): void
}
```

## Index Signature

```typescript
interface StringMap {
  [key: string]: string
}
```

## Generic Interfaces

```typescript
interface Container<T> {
  value: T
  getValue(): T
}

class Box<T> implements Container<T> {
  constructor(public value: T) {}
  
  getValue(): T {
    return this.value
  }
}
```
