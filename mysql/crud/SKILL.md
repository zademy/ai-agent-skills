---
name: crud
description: CRUD operations in MySQL
---

# MySQL CRUD Operations

## Create (Insert)

```sql
INSERT INTO users (name, email, password, created_at)
VALUES ('john', 'john@example.com', SHA2('password123', 256), NOW());

INSERT INTO orders (user_id, product_id, quantity, total)
VALUES
  (1, 1, 2, 99.99),
  (1, 2, 1, 49.99);
```

## Read (Select)

```sql
-- Basic
SELECT * FROM users WHERE id = 1;
SELECT name, email FROM users WHERE active = 1;

-- With conditions
SELECT * FROM products
WHERE price BETWEEN 10 AND 100
AND category = 'electronics';

-- With joins
SELECT u.name, p.title, o.quantity
FROM users u
INNER JOIN orders o ON u.id = o.user_id
INNER JOIN products p ON o.product_id = p.id
WHERE o.status = 'pending';
```

## Update

```sql
UPDATE users
SET name = 'John Doe', email = 'john.doe@example.com'
WHERE id = 1;

UPDATE products
SET price = price * 1.1
WHERE category = 'sale' AND active = 1;
```

## Delete

```sql
DELETE FROM users WHERE id = 1;
DELETE FROM sessions WHERE expires_at < NOW();
```

## Transactions

```sql
START TRANSACTION;
INSERT INTO orders (user_id, total) VALUES (1, 150.00);
UPDATE users SET balance = balance - 150.00 WHERE id = 1;
COMMIT;
```
