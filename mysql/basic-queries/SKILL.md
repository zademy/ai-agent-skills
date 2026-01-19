---
name: basic-queries
description: >
  Basic queries in MySQL.
  Trigger: When working with MySQL queries - SELECT, INSERT, UPDATE, DELETE, JOINs
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [database]
  auto_invoke: "MySQL Basic Queries / CRUD"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# MySQL Basic Queries

## SELECT

```sql
SELECT * FROM users;
SELECT id, name, email FROM users WHERE active = 1;
SELECT * FROM users ORDER BY created_at DESC LIMIT 10;
SELECT DISTINCT status FROM orders;
```

## INSERT

```sql
INSERT INTO users (name, email, age) VALUES ('John', 'john@example.com', 30);
INSERT INTO users (name, email) VALUES ('Jane', 'jane@example.com'), ('Bob', 'bob@example.com');
```

## UPDATE

```sql
UPDATE users SET name = 'John Doe' WHERE id = 1;
UPDATE users SET status = 'active', updated_at = NOW() WHERE id = 1;
```

## DELETE

```sql
DELETE FROM users WHERE id = 1;
DELETE FROM users WHERE status = 'inactive' AND created_at < '2024-01-01';
```

## JOINs

```sql
SELECT u.name, COUNT(o.id) as orders
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id;
```
