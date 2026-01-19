---
name: components
description: >
  Components in React with TypeScript and modern patterns.
  Trigger: When working with React components - functional components, props, children, Server/Client Components
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "React Components"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Components React

## Componente Funcional

```tsx
interface UserCardProps {
  name: string
  email: string
  avatar?: string
  onEdit: (id: string) => void
}

export function UserCard({ name, email, avatar, onEdit }: UserCardProps) {
  return (
    <div className="card">
      {avatar && <img src={avatar} alt={name} className="w-16 h-16 rounded-full" />}
      <h3 className="text-lg font-bold">{name}</h3>
      <p className="text-gray-600">{email}</p>
      <button
        onClick={() => onEdit(name)}
        className="px-4 py-2 bg-blue-500 text-white rounded"
      >
        Editar
      </button>
    </div>
  )
}
```

## Children y Slots

```tsx
interface ModalProps {
  isOpen: boolean
  onClose: () => void
  title?: string
  children: React.ReactNode
}

export function Modal({ isOpen, onClose, title, children }: ModalProps) {
  if (!isOpen) return null
  
  return (
    <div className="fixed inset-0 bg-black/50 flex items-center justify-center" onClick={onClose}>
      <div className="bg-white rounded-lg p-6 max-w-md w-full" onClick={e => e.stopPropagation()}>
        {title && <h2 className="text-xl font-bold mb-4">{title}</h2>}
        {children}
      </div>
    </div>
  )
}
```

## Server Components (Next.js)

```tsx
// Server Component - async por defecto
async function getData() {
  const res = await fetch('https://api.example.com/data', {
    next: { revalidate: 3600 } // Cache por 1 hora
  })
  return res.json()
}

export default async function Page() {
  const data = await getData()
  
  return (
    <div>
      <h1>Datos</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  )
}
```

## Client Components

```tsx
'use client'

import { useState } from 'react'

export function Counter({ initial = 0 }: { initial?: number }) {
  const [count, setCount] = useState(initial)
  
  return (
    <div className="flex gap-2 items-center">
      <span className="text-2xl font-bold">{count}</span>
      <button
        onClick={() => setCount(c => c + 1)}
        className="px-4 py-2 bg-green-500 text-white rounded"
      >
        +
      </button>
    </div>
  )
}
```
