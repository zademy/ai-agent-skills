---
name: promises
description: >
  Promises in JavaScript.
  Trigger: When working with Promises - Promise.all, Promise.race, chaining, states
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Promises / Async"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash, WebFetch, WebSearch
---

# JavaScript Promises

## Promise Basics

```javascript
const promise = new Promise((resolve, reject) => {
  const success = true;
  
  if (success) {
    resolve('Operation successful');
  } else {
    reject('Operation failed');
  }
});

promise
  .then(result => console.log(result))
  .catch(error => console.error(error));
```

## Promise States

```
Pending → Fulfilled (resolve) o Rejected (reject)
```

## Promise Static Methods

```javascript
// Wait for all promises
Promise.all([fetch(url1), fetch(url2), fetch(url3)])
  .then(results => console.log(results));

// Wait for first promise to complete
Promise.race([
  fetch(url1),
  new Promise(r => setTimeout(r, 5000))
])
  .then(result => console.log(result));

// Wait for all (first failure = immediate failure)
Promise.allSettled([
  fetch(url1),
  fetch(url2)
]).then(results => {
  results.forEach(result => {
    if (result.status === 'fulfilled') {
      console.log(result.value);
    } else {
      console.error(result.reason);
    }
  });
});

// Resolve with a value
Promise.resolve(42);

// Reject with a reason
Promise.reject(new Error('Failed'));
```

## Promise Chaining

```javascript
fetchData()
  .then(data => processData(data))
  .then(processed => saveData(processed))
  .then(() => console.log('Done'))
  .catch(error => console.error(error));

// Returning values in chain
fetchUser(1)
  .then(user => {
    return fetchOrders(user.id);
  })
  .then(orders => {
    console.log('User orders:', orders);
  });
```

## Async/Await ( syntactic sugar )

```javascript
async function getData() {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}

// Parallel async operations
async function getUsersAndOrders() {
  const [users, orders] = await Promise.all([
    fetchUsers(),
    fetchOrders()
  ]);
  return { users, orders };
}
```
