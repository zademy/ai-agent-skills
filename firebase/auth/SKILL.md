---
name: auth
description: Authentication with Firebase
---

# Firebase Authentication

## Setup

```javascript
import { initializeApp } from 'firebase/app'
import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, signOut, onAuthStateChanged } from 'firebase/auth'

const app = initializeApp(firebaseConfig)
const auth = getAuth(app)
```

## Sign Up

```javascript
async function signUp(email, password) {
  try {
    const userCredential = await createUserWithEmailAndPassword(auth, email, password)
    const user = userCredential.user
    console.log('User created:', user.uid)
  } catch (error) {
    console.error('Error:', error.message)
  }
}
```

## Sign In

```javascript
async function signIn(email, password) {
  try {
    const userCredential = await signInWithEmailAndPassword(auth, email, password)
    const user = userCredential.user
    console.log('Signed in:', user.email)
  } catch (error) {
    console.error('Error:', error.message)
  }
}
```

## Sign Out

```javascript
async function logOut() {
  try {
    await signOut(auth)
    console.log('Signed out successfully')
  } catch (error) {
    console.error('Error:', error.message)
  }
}
```

## Auth State Listener

```javascript
onAuthStateChanged(auth, (user) => {
  if (user) {
    console.log('User is signed in:', user.uid)
  } else {
    console.log('User is signed out')
  }
})
```

## Social Auth (Google)

```javascript
import { GoogleAuthProvider, signInWithPopup } from 'firebase/auth'

async function signInWithGoogle() {
  const provider = new GoogleAuthProvider()
  try {
    const result = await signInWithPopup(auth, provider)
    const user = result.user
    console.log('Google sign in:', user.displayName)
  } catch (error) {
    console.error('Error:', error.message)
  }
}
```
