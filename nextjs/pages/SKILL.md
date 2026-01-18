---
name: pages
description: Pages in Next.js 15 with App Router
---

# Páginas Next.js 15 (App Router)

## Page Component

```tsx
// app/page.tsx
export default async function HomePage() {
  const data = await fetch('https://api.example.com/data', {
    next: { revalidate: 3600 }
  }).then(res => res.json())
  
  return (
    <main>
      <h1>Bienvenido</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </main>
  )
}
```

## Dynamic Routes

```tsx
// app/users/[id]/page.tsx
interface Props {
  params: { id: string }
}

export default async function UserPage({ params }: Props) {
  const user = await fetch(`/api/users/${params.id}`).then(r => r.json())
  
  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  )
}
```

## Server Components (default)

```tsx
// Server Component
export default async function Page() {
  const data = await db.query('SELECT * FROM users')
  return <div>{data.length} usuarios</div>
}
```

## Client Components

```tsx
'use client'

import { useState } from 'react'

export function Counter() {
  const [count, setCount] = useState(0)
  return <button onClick={() => setCount(c => c + 1)}>{count}</button>
}
```
