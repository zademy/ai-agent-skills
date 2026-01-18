---
name: arrays
description: Array methods in JavaScript
---

# Arrays JavaScript

## Transformación

```javascript
const numbers = [1, 2, 3, 4, 5]

const doubled = numbers.map(n => n * 2)
const filtered = numbers.filter(n => n % 2 === 0)
const sum = numbers.reduce((a, b) => a + b, 0)
```

## Búsqueda

```javascript
const users = [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }]

const user = users.find(u => u.id === 1)
const index = users.findIndex(u => u.name === 'Jane')
const hasAdmin = users.some(u => u.role === 'admin')
const allActive = users.every(u => u.isActive)
```

## Ordenamiento

```javascript
const numbers = [3, 1, 4, 1, 5]
numbers.sort((a, b) => a - b)
```
