---
name: state-management
description: >
  State Management in React.
  Trigger: When working with state management - useState, useReducer, useContext, Zustand, Jotai
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "State Management / Store"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# React State Management

## useState

```typescript
import { useState } from 'react'

function Counter() {
  const [count, setCount] = useState(0)
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  )
}

// Object state
const [form, setForm] = useState({ name: '', email: '' })
setForm(prev => ({ ...prev, email: 'new@email.com' }))
```

## useReducer

```typescript
import { useReducer } from 'react'

type Action =
  | { type: 'INCREMENT' }
  | { type: 'DECREMENT' }
  | { type: 'RESET' }

function reducer(state: number, action: Action): number {
  switch (action.type) {
    case 'INCREMENT': return state + 1
    case 'DECREMENT': return state - 1
    case 'RESET': return 0
    default: return state
  }
}

function Counter() {
  const [count, dispatch] = useReducer(reducer, 0)
  
  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
    </>
  )
}
```

## useContext

```typescript
// Context
const ThemeContext = createContext('light')

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  )
}

function Toolbar() {
  const theme = useContext(ThemeContext)
  return <div theme={theme}>Toolbar</div>
}
```

## useRef

```typescript
import { useRef } from 'react'

function TextInput() {
  const inputRef = useRef<HTMLInputElement>(null)
  
  const focusInput = () => {
    inputRef.current?.focus()
  }
  
  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus</button>
    </>
  )
}
```

## useCallback

```typescript
const handleSubmit = useCallback((data: FormData) => {
  console.log(data)
}, [dependencies])
```

## useMemo

```typescript
const expensiveValue = useMemo(() => {
  return computeExpensiveValue(a, b)
}, [a, b])
```

## External Libraries

```typescript
// Zustand
import { create } from 'zustand'

const useStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 }))
}))

function Counter() {
  const { count, increment } = useStore()
  return <button onClick={increment}>{count}</button>
}

// Jotai
import { atom, useAtom } from 'jotai'

const countAtom = atom(0)

function Counter() {
  const [count, setCount] = useAtom(countAtom)
  return <button onClick={() => setCount(c => c + 1)}>{count}</button>
}
```
