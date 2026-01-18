---
name: caching
description: Caching patterns with Redis
---

# Redis Caching Patterns

## Cache-Aside

```javascript
async function getUser(id) {
  // 1. Check cache first
  const cached = await redis.get(`user:${id}`)
  if (cached) return JSON.parse(cached)
  
  // 2. Fetch from database
  const user = await db.users.findById(id)
  
  // 3. Store in cache
  await redis.setex(`user:${id}`, 3600, JSON.stringify(user))
  
  return user
}

async function updateUser(id, data) {
  // 1. Update database
  await db.users.update(id, data)
  
  // 2. Invalidate cache
  await redis.del(`user:${id}`)
}
```

## Session Store

```javascript
const session = {
  userId: '123',
  expiresAt: Date.now() + 86400000
}

await redis.setex(
  `session:${sessionId}`,
  86400,
  JSON.stringify(session)
)
```

## Rate Limiting

```javascript
const rateLimit = async (key, limit = 100, window = 60) => {
  const current = await redis.incr(`ratelimit:${key}`)
  if (current === 1) {
    await redis.expire(`ratelimit:${key}`, window)
  }
  return { allowed: current <= limit, remaining: Math.max(0, limit - current) }
}
```

## Pub/Sub

```javascript
// Publisher
await redis.publish('notifications', JSON.stringify({
  type: 'user_registered',
  data: { userId: 123 }
}));

// Subscriber
const subscriber = redis.duplicate()
await subscriber.subscribe('notifications', (message) => {
  console.log('Received:', message)
})
```
