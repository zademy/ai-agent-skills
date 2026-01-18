---
name: utilities
description: Utility Types in TypeScript
---

# TypeScript Utility Types

## Partial

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}

type PartialUser = Partial<User>;
// Todos los campos son opcionales
```

## Required

```typescript
type RequiredUser = Required<PartialUser>;
// Todos los campos son requeridos (invierte Partial)
```

## Pick

```typescript
type UserBasicInfo = Pick<User, 'id' | 'name'>;
// { id: number; name: string; }
```

## Omit

```typescript
type UserWithoutEmail = Omit<User, 'email'>;
// { id: number; name: string; age: number; }
```

## Record

```typescript
type UserMap = Record<string, User>;
// { [key: string]: User }

const users: UserMap = {
  'user1': { id: 1, name: 'John', email: 'john@email.com', age: 30 }
};
```

## Exclude

```typescript
type Status = 'pending' | 'approved' | 'rejected' | 'draft';
type ActiveStatus = Exclude<Status, 'draft'>;
// 'pending' | 'approved' | 'rejected'
```

## Extract

```typescript
type SuccessStatus = Extract<Status, 'pending' | 'approved'>;
// 'pending' | 'approved'
```

## NonNullable

```typescript
type MaybeString = string | null | undefined;
type NonNullString = NonNullable<MaybeString>;
// string
```

## ReturnType

```typescript
function getUser() {
  return { id: 1, name: 'John' };
}

type User = ReturnType<typeof getUser>;
// { id: number; name: string; }
```

## Parameters

```typescript
function greet(name: string, age: number): string {
  return `Hello ${name}, you are ${age} years old`;
}

type GreetParams = Parameters<typeof greet>;
// [string, number]
```

## ConstructorParameters

```typescript
class User {
  constructor(name: string, age: number) {}
}

type UserConstructorParams = ConstructorParameters<typeof User>;
// [string, number]
```

## Readonly

```typescript
type ReadonlyUser = Readonly<User>;
// Todos los campos son readonly
```

## Capitalize, Lowercase, Uppercase

```typescript
type LowerName = Lowercase<'HELLO'>; // 'hello'
type UpperName = Uppercase<'hello'>; // 'HELLO'
type Capitalized = Capitalize<'hello'>; // 'Hello'
```
