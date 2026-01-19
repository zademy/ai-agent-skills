---
name: async-await
description: >
  Async/Await in JavaScript.
  Trigger: When working with asynchronous operations - API calls, async functions, error handling
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Async / Promises / API"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash, WebFetch, WebSearch
---

# Async/Await JavaScript

## Async Function

```javascript
async function fetchData() {
  const response = await fetch('/api/data')
  const data = await response.json()
  return data
}

// Arrow function async
const fetchUsers = async () => {
  const res = await fetch('/api/users')
  return res.json()
}
```

## Try/Catch

```javascript
async function getData() {
  try {
    const response = await fetch('/api/data')
    if (!response.ok) throw new Error('Error en la solicitud')
    const data = await response.json()
    return data
  } catch (error) {
    console.error('Error:', error)
    throw error
  }
}
```

## Parallel Execution

```javascript
async function getAllData() {
  const [users, posts, comments] = await Promise.all([
    fetch('/api/users').then(r => r.json()),
    fetch('/api/posts').then(r => r.json()),
    fetch('/api/comments').then(r => r.json())
  ])
  return { users, posts, comments }
}
```
