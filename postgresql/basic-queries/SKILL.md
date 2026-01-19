---
name: basic-queries
description: >
  Basic queries in PostgreSQL.
  Trigger: When working with basic SQL queries - SELECT, INSERT, UPDATE, DELETE, JOINs
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [database]
  auto_invoke: "PostgreSQL Basic Queries / CRUD"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# PostgreSQL Basic Queries

## SELECT

```sql
-- Seleccionar columnas
SELECT id, name, email FROM users;

-- Seleccionar todos
SELECT * FROM users;

-- Con alias
SELECT id AS user_id, name AS user_name FROM users;

-- Distinct
SELECT DISTINCT status FROM orders;
```

## WHERE

```sql
SELECT * FROM users WHERE age >= 18;
SELECT * FROM users WHERE name LIKE 'J%';
SELECT * FROM users WHERE email ILIKE '%@example.com';
SELECT * FROM users WHERE id IN (1, 2, 3);
SELECT * FROM users WHERE age BETWEEN 18 AND 30;
```

## INSERT

```sql
INSERT INTO users (name, email, age)
VALUES ('John', 'john@example.com', 30);

INSERT INTO users (name, email)
VALUES ('Jane', 'jane@example.com'),
       ('Bob', 'bob@example.com');
```

## UPDATE

```sql
UPDATE users
SET name = 'John Doe', age = 31
WHERE id = 1;

UPDATE users
SET status = 'ACTIVE'
WHERE created_at > '2024-01-01';
```

## DELETE

```sql
DELETE FROM users WHERE id = 1;
DELETE FROM users WHERE status = 'INACTIVE';
```

## JOINs

```sql
SELECT u.name, o.order_date, o.total
FROM users u
INNER JOIN orders o ON u.id = o.user_id;

SELECT u.name, COUNT(o.id) as order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id;
```
