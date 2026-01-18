---
name: advanced-queries
description: Advanced queries in PostgreSQL
---

# PostgreSQL Advanced Queries

## Aggregations

```sql
-- COUNT
SELECT COUNT(*) FROM users;
SELECT COUNT(DISTINCT status) FROM users;

-- SUM, AVG, MIN, MAX
SELECT SUM(total) FROM orders;
SELECT AVG(age) FROM users;

-- GROUP BY
SELECT status, COUNT(*)
FROM users
GROUP BY status;

-- HAVING
SELECT user_id, COUNT(*) as orders
FROM orders
GROUP BY user_id
HAVING COUNT(*) > 5;
```

## Subqueries

```sql
-- En WHERE
SELECT name FROM users
WHERE id IN (SELECT user_id FROM orders WHERE total > 1000);

-- En FROM
SELECT AVG(total) FROM (
    SELECT user_id, SUM(total) as total
    FROM orders
    GROUP BY user_id
) as user_totals;
```

## Window Functions

```sql
-- ROW_NUMBER
SELECT
  name,
  age,
  ROW_NUMBER() OVER (ORDER BY age DESC) as rank
FROM users;

-- PARTITION BY
SELECT
  name,
  department,
  salary,
  AVG(salary) OVER (PARTITION BY department) as dept_avg
FROM employees;
```

## Transactions

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;

-- Con savepoint
BEGIN;
INSERT INTO orders (...) VALUES (...);
SAVEPOINT order_saved;
UPDATE inventory SET stock = stock - 1 WHERE product_id = 1;
ROLLBACK TO SAVEPOINT order_saved;
COMMIT;
```

## CTEs

```sql
WITH active_users AS (
    SELECT * FROM users WHERE status = 'ACTIVE'
)
SELECT * FROM active_users WHERE age >= 18;
```
