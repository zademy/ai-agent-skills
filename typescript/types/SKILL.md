---
name: types
description: >
  Basic types in TypeScript.
  Trigger: When working with TypeScript types - primitives, unions, intersections, literals, type aliases
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "TypeScript Types"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# TypeScript Types

## Basic Types

```typescript
// Primitivos
let name: string = 'John';
let age: number = 30;
let isActive: boolean = true;

// Array
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ['John', 'Jane'];

// Tuple
let tuple: [string, number] = ['John', 30];

// Enum
enum Status {
  Pending = 'PENDING',
  Approved = 'APPROVED',
  Rejected = 'REJECTED'
}

// Any (evitar usar)
let anything: any = 42;

// Unknown (tipo seguro)
let unknownValue: unknown = 'hello';
if (typeof unknownValue === 'string') {
  console.log(unknownValue.toUpperCase());
}

// Void (funciones sin retorno)
function logMessage(message: string): void {
  console.log(message);
}

// Never (nunca retorna)
function throwError(message: string): never {
  throw new Error(message);
}
```

## Type Aliases

```typescript
type Point = {
  x: number;
  y: number;
};

type ID = string | number;

type Callback = (data: string) => void;
```

## Union Types

```typescript
let id: string | number;
id = 'abc123';
id = 123;

function formatId(id: string | number): string {
  return `ID: ${id}`;
}
```

## Intersection Types

```typescript
type Admin = {
  adminLevel: number;
};

type Employee = {
  employeeId: string;
};

type AdminEmployee = Admin & Employee;

const admin: AdminEmployee = {
  adminLevel: 1,
  employeeId: 'E123'
};
```

## Literal Types

```typescript
type Direction = 'north' | 'south' | 'east' | 'west';

function move(direction: Direction): void {
  console.log(`Moving ${direction}`);
}
```

## Type Inference

```typescript
// TypeScript infiere el tipo automáticamente
let message = 'Hello'; // string
let count = 42; // number
```

## Type Assertions

```typescript
let value: unknown = 'hello';

// Angle bracket (no funciona en .tsx)
let strLength1: number = (<string>value).length;

// as syntax
let strLength2: number = (value as string).length;

// Non-null assertion
let element: HTMLElement | null = document.getElementById('app');
let app: HTMLElement = element!;
```
