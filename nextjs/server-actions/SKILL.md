---
name: server-actions
description: >
  Server Actions in Next.js.
  Trigger: When working with Server Actions - form submissions, mutations, useFormState, revalidatePath, redirect
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Server Actions / Mutations"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Next.js Server Actions

## Basic Server Action

```typescript
// app/actions.ts
'use server'

export async function createUser(formData: FormData) {
  const name = formData.get('name')
  const email = formData.get('email')
  
  await db.user.create({
    data: { name: String(name), email: String(email) }
  })
  
  revalidatePath('/users')
}
```

## Server Action in Component

```typescript
// app/form.tsx
'use client'

import { createUser } from './actions'

export default function UserForm() {
  return (
    <form action={createUser}>
      <input name="name" type="text" />
      <input name="email" type="email" />
      <button type="submit">Create</button>
    </form>
  )
}
```

## Server Action with Validation

```typescript
// app/actions.ts
'use server'

import { z } from 'zod'

const schema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
})

export async function createUser(prevState: any, formData: FormData) {
  const data = {
    name: formData.get('name'),
    email: formData.get('email'),
  }
  
  const result = schema.safeParse(data)
  
  if (!result.success) {
    return { errors: result.error.flatten().fieldErrors }
  }
  
  await db.user.create({ data: result.data })
  
  return { message: 'User created!' }
}
```

## UseFormState

```typescript
// app/form.tsx
'use client'

import { useFormState } from 'react-dom'
import { createUser } from './actions'

const initialState = { message: '', errors: {} }

export default function UserForm() {
  const [state, formAction] = useFormState(createUser, initialState)
  
  return (
    <form action={formAction}>
      <input name="name" />
      {state.errors?.name && <span>{state.errors.name}</span>}
      
      <input name="email" />
      {state.errors?.email && <span>{state.errors.email}</span>}
      
      <button type="submit">Submit</button>
      
      {state.message && <p>{state.message}</p>}
    </form>
  )
}
```

## Server Action with Cache

```typescript
// app/actions.ts
'use server'

import { cache } from 'react'

export const getUser = cache(async (id: string) => {
  return db.user.findUnique({ where: { id } })
})
```

## Mutation with Revalidate

```typescript
// app/actions.ts
'use server'

export async function updatePost(id: string, data: PostData) {
  await db.post.update({
    where: { id },
    data
  })
  
  revalidatePath(`/posts/${id}`)
  revalidatePath('/posts')
}
```

## Redirect in Server Action

```typescript
// app/actions.ts
'use server'

import { redirect } from 'next/navigation'

export async function login(formData: FormData) {
  const email = formData.get('email')
  
  if (email === 'admin@example.com') {
    redirect('/admin')
  }
  
  return { error: 'Invalid email' }
}
```

## Private Server Action

```typescript
// app/actions.ts
'use server'

export async function protectedAction() {
  const session = await getSession()
  
  if (!session?.user) {
    throw new Error('Unauthorized')
  }
  
  return { success: true }
}
```
