---
name: firestore
description: >
  CRUD operations in Firebase Firestore.
  Trigger: When working with Firestore - addDoc, getDoc, getDocs, updateDoc, deleteDoc, queries
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [database]
  auto_invoke: "Firebase Firestore / NoSQL"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Firebase Firestore CRUD

## Setup

```javascript
import { initializeApp } from 'firebase/app'
import { getFirestore, collection, doc, getDoc, getDocs, addDoc, updateDoc, deleteDoc, query, where, orderBy } from 'firebase/firestore'

const app = initializeApp(firebaseConfig)
const db = getFirestore(app)
```

## Create

```javascript
// Add document with auto-ID
const docRef = await addDoc(collection(db, 'users'), {
  name: 'John',
  email: 'john@example.com',
  age: 30,
  createdAt: new Date()
})
console.log('Created:', docRef.id)

// With custom ID
await setDoc(doc(db, 'users', 'user123'), {
  name: 'Jane',
  email: 'jane@example.com'
})
```

## Read

```javascript
// Get single document
const docSnap = await getDoc(doc(db, 'users', 'user123'))
if (docSnap.exists()) {
  console.log('User:', docSnap.data())
}

// Get all from collection
const querySnapshot = await getDocs(collection(db, 'users'))
querySnapshot.forEach(doc => {
  console.log(doc.id, doc.data())
})

// With query
const q = query(
  collection(db, 'users'),
  where('age', '>=', 18),
  orderBy('name')
)
```

## Update

```javascript
const userRef = doc(db, 'users', 'user123')
await updateDoc(userRef, {
  name: 'John Doe',
  updatedAt: new Date()
})

// Increment
await updateDoc(userRef, {
  age: increment(1)
})
```

## Delete

```javascript
await deleteDoc(doc(db, 'users', 'user123'))

// Delete collection (server-side)
```
