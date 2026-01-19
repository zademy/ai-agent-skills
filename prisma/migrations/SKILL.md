---
name: migrations
description: >
  Migrations in Prisma.
  Trigger: When managing Prisma migrations - migrate dev, deploy, reset, seed, custom SQL
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [database]
  auto_invoke: "Prisma Migrations / DB Management"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Prisma Migrations

## Create Migration

```bash
# After modifying schema.prisma
npx prisma migrate dev --name init

# Or for a specific name
npx prisma migrate dev --name add_user_profile
```

## Migration Commands

```bash
# Create and apply migration (development)
npx prisma migrate dev

# Apply migrations (production)
npx prisma migrate deploy

# Reset database (development only!)
npx prisma migrate reset

# Status of migrations
npx prisma migrate status

# Show applied migrations
npx prisma migrate list

# Reset - skip confirm
npx prisma migrate reset --skip-generate
```

## Generate Client

```bash
# Generate after schema changes
npx prisma generate

# With specific schema
npx prisma generate --schema=./prisma/schema.prisma
```

## Seed Database

```typescript
// prisma/seed.ts
import { PrismaClient } from '@prisma/client'

const prisma = new PrismaClient()

async function main() {
  const user = await prisma.user.create({
    data: {
      email: 'admin@example.com',
      name: 'Admin',
      role: 'ADMIN'
    }
  })
  console.log({ user })
}

main()
  .then(async () => {
    await prisma.$disconnect()
  })
  .catch(async (e) => {
    console.error(e)
    await prisma.$disconnect()
    process.exit(1)
  })
```

```json
// package.json
{
  "prisma": {
    "seed": "ts-node prisma/seed.ts"
  }
}
```

## Migration History

```bash
# View applied migrations
npx prisma migrate list

# Create empty migration for custom SQL
npx prisma migrate dev --name add_custom_index --create-only
```

## Custom SQL in Migration

```sql
-- migrations/20240101000000_add_custom_index/migration.sql
CREATE INDEX CONCURRENTLY idx_user_email ON users(email);

-- Only run on create
CREATE OR REPLACE FUNCTION execute_if_exists()
RETURNS void AS $$
BEGIN
  IF EXISTS (SELECT 1 FROM pg_indexes WHERE indexname = 'idx_user_email') THEN
    RAISE NOTICE 'Index already exists';
  ELSE
    CREATE INDEX CONCURRENTLY idx_user_email ON users(email);
  END IF;
END;
$$ LANGUAGE plpgsql;

SELECT execute_if_exists();
```
