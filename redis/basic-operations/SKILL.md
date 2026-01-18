---
name: basic-operations
description: Basic operations in Redis
---

# Redis Basic Operations

## Strings

```bash
SET user:1 "John"
GET user:1
DEL user:1
INCR counter
DECR counter
APPEND key "value"
```

## Hashes

```bash
HSET user:1 name "John" email "john@example.com" age "30"
HGET user:1 name
HGETALL user:1
HDEL user:1 age
HEXISTS user:1 name
```

## Lists

```bash
LPUSH mylist "item1"
RPUSH mylist "item2"
LRANGE mylist 0 -1
LPOP mylist
RPOP mylist
LLEN mylist
```

## Sets

```bash
SADD tags "javascript" "react" "node"
SMEMBERS tags
SISMEMBER tags "react"
SREM tags "node"
SCARD tags
```

## Sorted Sets

```bash
ZADD leaderboard 100 "player1" 200 "player2" 150 "player3"
ZRANGE leaderboard 0 -1 WITHSCORES
ZREVRANGE leaderboard 0 10
ZSCORE leaderboard "player1"
```

## Keys

```bash
KEYS user:*
EXPIRE key 3600
TTL key
PERSIST key
TYPE key
```
