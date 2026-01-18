---
name: queries
description: Queries with Prisma Client
---

# Prisma Queries

## CRUD Basic

```typescript
import { PrismaClient } from '@prisma/client'
const prisma = new PrismaClient()

// Create
const user = await prisma.user.create({
  data: {
    email: 'john@example.com',
    name: 'John'
  }
})

// Read all
const users = await prisma.user.findMany()

// Read one
const user = await prisma.user.findUnique({
  where: { id: 1 }
})

// Update
const updated = await prisma.user.update({
  where: { id: 1 },
  data: { name: 'Jane' }
})

// Delete
await prisma.user.delete({
  where: { id: 1 }
})
```

## Queries Avanzadas

```typescript
// Where con condiciones
const users = await prisma.user.findMany({
  where: {
    email: { contains: '@example.com' },
    age: { gte: 18 },
    status: 'ACTIVE'
  },
  orderBy: { createdAt: 'desc' },
  take: 10,
  skip: 0
})

// Include relaciones
const posts = await prisma.post.findMany({
  where: { published: true },
  include: {
    author: true,
    tags: true
  }
})

// Aggregations
const stats = await prisma.user.aggregate({
  where: { status: 'ACTIVE' },
  _count: { id: true },
  _avg: { age: true }
})

// Group By
const grouped = await prisma.post.groupBy({
  by: ['authorId'],
  _count: { id: true }
})
```
