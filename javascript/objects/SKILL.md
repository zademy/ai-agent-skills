---
name: objects
description: Objects in JavaScript
---

# JavaScript Objects

## Object Literal

```javascript
const user = {
  name: 'John',
  age: 30,
  'special-key': 'value', // Key with special char
  sayHello() {
    return `Hello, ${this.name}`;
  }
};

// Access
console.log(user.name);
console.log(user['age']);

// Dynamic access
const key = 'name';
console.log(user[key]);
```

## Object Methods

```javascript
const person = {
  firstName: 'John',
  lastName: 'Doe',
  
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  }
};

console.log(person.fullName); // "John Doe"
person.fullName = 'Jane Smith';
console.log(person.firstName); // "Jane"
```

## Object Destructuring

```javascript
const user = { name: 'John', age: 30, city: 'NYC' };

// Basic
const { name, age } = user;

// With new names
const { name: userName, age: userAge } = user;

// Default values
const { name = 'Anonymous', country = 'USA' } = user;

// Rest operator
const { name, ...rest } = user;
console.log(rest); // { age: 30, city: 'NYC' }
```

## Object.entries y Object.values

```javascript
const obj = { a: 1, b: 2, c: 3 };

Object.values(obj); // [1, 2, 3]
Object.entries(obj); // [['a', 1], ['b', 2], ['c', 3]]

// Iterating
for (const [key, value] of Object.entries(obj)) {
  console.log(`${key}: ${value}`);
}
```

## Object.freeze y Object.seal

```javascript
const obj = { a: 1 };

Object.freeze(obj); // No changes allowed
Object.seal(obj); // Can modify existing properties, can't add new ones
```

## Spread y Merge

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };

// Merge
const merged = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3, d: 4 }

// Clone
const clone = { ...obj1 };

// Override
const updated = { ...obj1, b: 99 };
```
