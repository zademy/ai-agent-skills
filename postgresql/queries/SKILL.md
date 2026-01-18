---
name: queries
description: PostgreSQL queries
---

# PostgreSQL Queries

## Basic SELECT

```sql
-- Select all columns
SELECT * FROM users;

-- Select specific columns
SELECT id, name, email FROM users;

-- With WHERE clause
SELECT * FROM users WHERE age >= 18;

-- With LIKE
SELECT * FROM users WHERE email LIKE '%@gmail.com';

-- With IN
SELECT * FROM users WHERE country IN ('USA', 'Canada', 'Mexico');

-- With BETWEEN
SELECT * FROM orders WHERE total BETWEEN 100 AND 500;
```

## JOINs

```sql
-- INNER JOIN
SELECT u.name, o.order_date, o.total
FROM users u
INNER JOIN orders o ON u.id = o.user_id;

-- LEFT JOIN
SELECT u.name, o.order_date, o.total
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;

-- RIGHT JOIN
SELECT u.name, o.order_date, o.total
FROM orders o
RIGHT JOIN users u ON u.id = o.user_id;

-- FULL OUTER JOIN
SELECT u.name, o.order_date
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;

-- Multiple JOINs
SELECT u.name, o.order_date, p.name as product
FROM users u
INNER JOIN orders o ON u.id = o.user_id
INNER JOIN order_items oi ON o.id = oi.order_id
INNER JOIN products p ON oi.product_id = p.id;
```

## Aggregations

```sql
-- COUNT
SELECT COUNT(*) FROM users;

-- SUM
SELECT SUM(total) FROM orders;

-- AVG
SELECT AVG(age) FROM users;

-- MIN/MAX
SELECT MIN(price), MAX(price) FROM products;

-- GROUP BY
SELECT country, COUNT(*)
FROM users
GROUP BY country;

-- HAVING
SELECT country, COUNT(*) as total
FROM users
GROUP BY country
HAVING COUNT(*) > 100;

-- GROUP BY con múltiples columnas
SELECT country, status, COUNT(*)
FROM users
GROUP BY country, status;
```

## Subqueries

```sql
-- IN subquery
SELECT * FROM products
WHERE id IN (
  SELECT product_id FROM order_items WHERE quantity > 5
);

-- EXISTS subquery
SELECT * FROM users u
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.user_id = u.id
);

-- Correlated subquery
SELECT u.name, (
  SELECT COUNT(*) FROM orders o WHERE o.user_id = u.id
) as order_count
FROM users u;
```

## CASE Expression

```sql
SELECT
  name,
  age,
  CASE
    WHEN age < 18 THEN 'Minor'
    WHEN age < 65 THEN 'Adult'
    ELSE 'Senior'
  END as age_group
FROM users;

-- CASE en UPDATE
UPDATE users
SET status = CASE
  WHEN total_orders > 100 THEN 'VIP'
  WHEN total_orders > 50 THEN 'Premium'
  ELSE 'Regular'
END;
```

## Window Functions

```sql
-- ROW_NUMBER
SELECT
  name,
  ROW_NUMBER() OVER (ORDER BY created_at DESC) as rn
FROM users;

-- RANK
SELECT
  name,
  RANK() OVER (ORDER BY score DESC) as rank
FROM users;

-- PARTITION BY
SELECT
  country,
  name,
  ROW_NUMBER() OVER (PARTITION BY country ORDER BY score DESC) as rn
FROM users;

-- Running total
SELECT
  date,
  amount,
  SUM(amount) OVER (ORDER BY date) as running_total
FROM transactions;
```

## Common Table Expressions (CTE)

```sql
-- Basic CTE
WITH active_users AS (
  SELECT * FROM users WHERE status = 'active'
)
SELECT * FROM active_users WHERE country = 'USA';

-- Recursive CTE
WITH RECURSIVE hierarchy AS (
  SELECT id, name, manager_id, 0 as level
  FROM employees WHERE manager_id IS NULL
  UNION ALL
  SELECT e.id, e.name, e.manager_id, h.level + 1
  FROM employees e
  INNER JOIN hierarchy h ON e.manager_id = h.id
)
SELECT * FROM hierarchy;
```
