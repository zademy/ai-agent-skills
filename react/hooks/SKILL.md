---
name: hooks
description: React Hooks with React 19 and updated TypeScript
---

# React Hooks (React 19)

## useState

```tsx
import { useState } from 'react'

// Tipado con TypeScript
function Counter({ initial = 0 }: { initial?: number }) {
  const [count, setCount] = useState<number>(initial)
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(c => c + 1)}>+</button>
      <button onClick={() => setCount(c => c - 1)}>-</button>
    </div>
  )
}
```

## useEffect

```tsx
import { useEffect, useState } from 'react'

interface User {
  id: number
  name: string
}

function UserList() {
  const [users, setUsers] = useState<User[]>([])
  
  useEffect(() => {
    const controller = new AbortController()
    
    fetch('/api/users', { signal: controller.signal })
      .then(res => res.json())
      .then(setUsers)
      .catch(err => {
        if (err.name !== 'AbortError') {
          console.error(err)
        }
      })
    
    return () => controller.abort()
  }, [])
  
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  )
}
```

## useRef

```tsx
import { useRef, useEffect } from 'react'

function usePrevious<T>(value: T): T | undefined {
  const ref = useRef<T>()
  
  useEffect(() => {
    ref.current = value
  }, [value])
  
  return ref.current
}
```

## useCallback

```tsx
import { useCallback } from 'react'

function useHandler(fn: () => void) {
  return useCallback(fn, [fn])
}
```

## useMemo

```tsx
import { useMemo } from 'react'

function SortedList<T>({ items, compare }: {
  items: T[]
  compare: (a: T, b: T) => number
}) {
  const sorted = useMemo(() =>
    [...items].sort(compare),
    [items, compare]
  )
  
  return sorted.map((item, i) => <li key={i}>{String(item)}</li>)
}
```

## useContext

```tsx
import { createContext, useContext } from 'react'

interface AuthContextType {
  user: User | null
  login: (user: User) => void
  logout: () => void
}

const AuthContext = createContext<AuthContextType | null>(null)

export function AuthProvider({ children }: { children: React.ReactNode }) {
  const [user, setUser] = useState<User | null>(null)
  
  return (
    <AuthContext.Provider value={{
      user,
      login: setUser,
      logout: () => setUser(null)
    }}>
      {children}
    </AuthContext.Provider>
  )
}

export function useAuth() {
  const context = useContext(AuthContext)
  if (!context) throw new Error('useAuth required')
  return context
}
```

## useId (React 18+)

```tsx
import { useId } from 'react'

function FormField({ label }: { label: string }) {
  const id = useId()
  
  return (
    <div>
      <label htmlFor={id}>{label}</label>
      <input id={id} type="text" />
    </div>
  )
}
```

## Custom Hooks

```tsx
// useFetch
function useFetch<T>(url: string) {
  const [data, setData] = useState<T | null>(null)
  const [loading, setLoading] = useState(true)
  const [error, setError] = useState<Error | null>(null)
  
  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false))
  }, [url])
  
  return { data, loading, error }
}

// useLocalStorage
function useLocalStorage<T>(key: string, initial: T) {
  const [value, setValue] = useState<T>(() => {
    if (typeof window === 'undefined') return initial
    const stored = localStorage.getItem(key)
    return stored ? JSON.parse(stored) : initial
  })
  
  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value))
  }, [key, value])
  
  return [value, setValue] as const
}
```
