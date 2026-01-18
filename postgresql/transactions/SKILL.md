---
name: transactions
description: Transactions in PostgreSQL
---

# PostgreSQL Transactions

## Basic Transaction

```sql
BEGIN;
-- Operations here
COMMIT;
-- or ROLLBACK;
```

## SAVEPOINT

```sql
BEGIN;

INSERT INTO accounts (name, balance) VALUES ('Alice', 1000);

SAVEPOINT sp1;

INSERT INTO accounts (name, balance) VALUES ('Bob', 500);

-- Rollback to savepoint
ROLLBACK TO sp1;

COMMIT;
```

## Transaction Isolation Levels

```sql
-- Read Committed (default)
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- Read Uncommitted
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;

-- Repeatable Read
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

-- Serializable
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

## WITH HOLD Cursor

```sql
BEGIN;
DECLARE my_cursor CURSOR FOR SELECT * FROM users;
FETCH NEXT FROM my_cursor;
-- Cursor persists after COMMIT
COMMIT;
```

## Advisory Locks

```sql
-- Get lock
SELECT pg_advisory_lock(12345);

-- Release lock
SELECT pg_advisory_unlock(12345);

-- Try lock (non-blocking)
SELECT pg_try_advisory_lock(12345);
```

## Row-level Locks

```sql
BEGIN;

-- Lock row for update
SELECT * FROM orders WHERE id = 1 FOR UPDATE;

-- Lock row with skip locked
SELECT * FROM orders FOR UPDATE SKIP LOCKED;

-- Lock row with nowait
SELECT * FROM orders FOR UPDATE NOWAIT;

COMMIT;
```
