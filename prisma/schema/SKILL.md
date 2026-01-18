---
name: schema
description: Schema in Prisma ORM
---

# Prisma Schema

## Esquema Básico

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
  updatedAt DateTime @updatedAt
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

## Relaciones

```prisma
// Uno a muchos
model User {
  posts Post[]
}

model Post {
  author   User @relation(fields: [authorId], references: [id])
  authorId Int
}

// Muchos a muchos
model Post {
  tags Tag[]
}

model Tag {
  posts Post[]
}

// Uno a uno
model User {
  profile Profile?
}

model Profile {
  user   User @relation(fields: [userId], references: [id])
  userId Int  @unique
}
```

## Atributos

```prisma
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String   @db.VarChar(100)
  age       Int?
  active    Boolean  @default(true)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  @@map("users")
  @@index([email])
}
```
