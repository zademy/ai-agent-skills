---
name: classes
description: Classes in TypeScript with access modifiers
---

# Classes TypeScript

## Clase Básica

```typescript
class User {
  id: number
  name: string
  email: string
  
  constructor(id: number, name: string, email: string) {
    this.id = id
    this.name = name
    this.email = email
  }
  
  greet(): string {
    return `Hola, ${this.name}`
  }
}
```

## Modificadores  in acceso

```typescript
class User {
  private id: number
  protected name: string
  public email: string
  readonly createdAt: Date
  
  constructor(id: number, name: string, email: string) {
    this.id = id
    this.name = name
    this.email = email
    this.createdAt = new Date()
  }
}
```

## Herencia

```typescript
class Admin extends User {
  role: string = 'admin'
  
  override greet(): string {
    return `Hola Admin ${this.name}`
  }
}
```

## Classes Abstractas

```typescript
abstract class Animal {
  abstract makeSound(): void
  
  sleep(): void {
    console.log('Dormiendo...')
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log('Guau!')
  }
}
```
