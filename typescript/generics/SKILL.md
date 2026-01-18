---
name: generics
description: Generics in TypeScript
---

# Generics TypeScript

## Función Genérica

```typescript
function identity<T>(value: T): T {
  return value
}

identity<string>('hello')
identity<number>(42)
```

## Interface Genérica

```typescript
interface Container<T> {
  value: T
}

class Box<T> implements Container<T> {
  constructor(public value: T) {}
}
```

## Restricciones

```typescript
interface HasLength {
  length: number
}

function logLength<T extends HasLength>(item: T): void {
  console.log(item.length)
}
```

## Utility Types

```typescript
interface User {
  id: number
  name: string
  email: string
  password: string
}

type PartialUser = Partial<User>
type UserPreview = Pick<User, 'id' | 'name' | 'email'>
type UserWithoutPassword = Omit<User, 'password'>
