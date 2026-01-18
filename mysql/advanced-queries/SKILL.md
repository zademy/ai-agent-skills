---
name: advanced-queries
description: Advanced queries in MySQL
---

# MySQL Advanced Queries

## Window Functions

```sql
-- ROW_NUMBER
SELECT
  name,
  ROW_NUMBER() OVER (ORDER BY created_at DESC) as row_num
FROM users;

-- RANK
SELECT
  name,
  score,
  RANK() OVER (ORDER BY score DESC) as rank
FROM users;

-- DENSE_RANK
SELECT
  name,
  score,
  DENSE_RANK() OVER (ORDER BY score DESC) as dense_rank
FROM users;

-- PARTITION BY
SELECT
  country,
  name,
  ROW_NUMBER() OVER (PARTITION BY country ORDER BY score DESC) as rank
FROM users;

-- Running total
SELECT
  date,
  amount,
  SUM(amount) OVER (ORDER BY date) as running_total
FROM orders;
```

## CTE (Common Table Expressions)

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

-- Multiple CTEs
WITH
  users_cte AS (SELECT * FROM users WHERE active = 1),
  orders_cte AS (SELECT * FROM orders WHERE status = 'completed')
SELECT u.name, COUNT(o.id) as order_count
FROM users_cte u
LEFT JOIN orders_cte o ON u.id = o.user_id
GROUP BY u.id;
```

## Case Expression

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

-- CASE in UPDATE
UPDATE users
SET status = CASE
  WHEN total_orders > 100 THEN 'VIP'
  WHEN total_orders > 50 THEN 'Premium'
  ELSE 'Regular'
END;
```

## Subqueries

```sql
-- Scalar subquery
SELECT name,
  (SELECT COUNT(*) FROM orders WHERE user_id = users.id) as order_count
FROM users;

-- IN subquery
SELECT * FROM products
WHERE category_id IN (
  SELECT id FROM categories WHERE name IN ('Electronics', 'Books')
);

-- EXISTS subquery
SELECT * FROM users u
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.user_id = u.id
);
```

## Index Optimization

```sql
-- Create index
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_user_date ON orders(user_id, created_at);

-- Composite index
CREATE INDEX idx_products_category_price ON products(category_id, price);

-- Unique index
CREATE UNIQUE INDEX idx_products_sku ON products(sku);

-- Full-text index
CREATE FULLTEXT INDEX idx_articles_title ON articles(title, body);

-- Use EXPLAIN to analyze queries
EXPLAIN SELECT * FROM users WHERE email = 'test@example.com';
```
