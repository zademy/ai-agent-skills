---
name: routing
description: Routing in Next.js
---

# Next.js Routing

## App Router (Next.js 13+)

```typescript
// app/page.tsx
export default function HomePage() {
  return <h1>Home Page</h1>
}

// app/about/page.tsx
export default function AboutPage() {
  return <h1>About Page</h1>
}

// app/blog/[slug]/page.tsx
interface Props {
  params: { slug: string }
}

export default function BlogPost({ params }: Props) {
  return <h1>Post: {params.slug}</h1>
}

// app/users/[id]/page.tsx
interface Props {
  params: { id: string }
}

export default function UserPage({ params }: Props) {
  return <h1>User: {params.id}</h1>
}
```

## Dynamic Routes

```typescript
// app/products/[category]/[id]/page.tsx
interface Props {
  params: {
    category: string
    id: string
  }
}

export default function ProductPage({ params }: Props) {
  return (
    <div>
      <h1>{params.category}</h1>
      <p>Product ID: {params.id}</p>
    </div>
  )
}
```

## Optional Params

```typescript
// app/blog/[[...slug]]/page.tsx
interface Props {
  params: { slug?: string[] }
}

export default function BlogPage({ params }: Props) {
  const slug = params.slug || []
  return <h1>Blog: {slug.join('/')}</h1>
}
```

## Route Groups

```typescript
// app/(marketing)/about/page.tsx
export default function AboutPage() {
  return <h1>About</h1>
}

// app/(dashboard)/settings/page.tsx
export default function SettingsPage() {
  return <h1>Settings</h1>
}
```

## Linking

```typescript
import Link from 'next/link'

export default function Navbar() {
  return (
    <nav>
      <Link href="/">Home</Link>
      <Link href="/about">About</Link>
      <Link href={`/users/${userId}`}>User Profile</Link>
    </nav>
  )
}
```

## useRouter

```typescript
'use client'

import { useRouter } from 'next/navigation'

export default function LoginButton() {
  const router = useRouter()
  
  async function handleLogin() {
    await login()
    router.push('/dashboard')
    router.refresh()
  }
  
  return <button onClick={handleLogin}>Login</button>
}
```

## Redirect

```typescript
// In Server Component
import { redirect } from 'next/navigation'

export default async function Page({ searchParams }: Props) {
  const session = await getSession()
  
  if (!session) {
    redirect('/login')
  }
  
  return <Dashboard />
}
```

## Parallel Routes

```typescript
// app/@modal/(.)login/page.tsx
export default function LoginModal() {
  return (
    <dialog>
      <h1>Login Modal</h1>
    </dialog>
  )
}

// app/layout.tsx
export default function Layout({ children, modal }: Props) {
  return (
    <>
      {children}
      {modal}
    </>
  )
}
```
