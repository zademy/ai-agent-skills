---
name: basics
description: Prisma basics
---

# Prisma Basics

## Setup

```bash
npm install prisma --save-dev
npm install @prisma/client

npx prisma init
```

## Schema

```prisma
// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

## Client Usage

```typescript
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

// Find all
const users = await prisma.user.findMany()

// Find one
const user = await prisma.user.findUnique({
  where: { id: 1 }
})

// Create
const user = await prisma.user.create({
  data: {
    email: 'john@example.com',
    name: 'John'
  }
})

// Update
const user = await prisma.user.update({
  where: { id: 1 },
  data: { name: 'John Doe' }
})

// Delete
await prisma.user.delete({
  where: { id: 1 }
})
```

## Relations

```typescript
// Include relations
const users = await prisma.user.findMany({
  include: {
    posts: true
  }
})

// Nested creates
await prisma.user.create({
  data: {
    email: 'john@example.com',
    posts: {
      create: {
        title: 'Hello World',
        content: 'My first post'
      }
    }
  }
})
```
