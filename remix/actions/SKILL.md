---
name: actions
description: >
  Actions in Remix.
  Trigger: When working with Remix actions - form handling, validation, sessions, file uploads
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [backend]
  auto_invoke: "Remix Actions / Mutations"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Remix Actions

## Basic Action

```typescript
import { ActionFunctionArgs, json, redirect } from '@remix-run/node'

export const action = async ({ request }: ActionFunctionArgs) => {
  const formData = await request.formData()
  const email = formData.get('email')
  const password = formData.get('password')
  
  // Validate
  if (!email || !password) {
    return json({ error: 'Email and password required' }, { status: 400 })
  }
  
  // Process
  await createUser(String(email), String(password))
  
  return redirect('/dashboard')
}
```

## Action with Validation

```typescript
import { z } from 'zod'

const schema = z.object({
  name: z.string().min(2),
  email: z.string().email(),
  age: z.number().min(18)
})

export const action = async ({ request }: ActionFunctionArgs) => {
  const formData = await request.formData()
  const data = Object.fromEntries(formData)
  
  const result = schema.safeParse(data)
  
  if (!result.success) {
    return json({ errors: result.error.flatten().fieldErrors }, { status: 400 })
  }
  
  await createUser(result.data)
  return json({ success: true })
}
```

## Action with Session

```typescript
import { createCookieSessionStorage } from '@remix-run/node'

const sessionStorage = createCookieSessionStorage({
  cookie: {
    name: '_session',
    secrets: ['s3cr3t'],
    path: '/'
  }
})

export const action = async ({ request }: ActionFunctionArgs) => {
  const session = await sessionStorage.getSession(request.headers.get('Cookie'))
  const formData = await request.formData()
  
  const userId = formData.get('userId')
  session.set('userId', userId)
  
  return json(null, {
    headers: { 'Set-Cookie': await sessionStorage.commitSession(session) }
  })
}
```

## Action with File Upload

```typescript
import { writeAsyncIterableToWritable } from '@remix-run/node'
import { unzip } from 'unzipit'

export const action = async ({ request }: ActionFunctionArgs) => {
  const formData = await request.formData()
  const file = formData.get('file') as File
  
  if (!file) {
    return json({ error: 'No file uploaded' }, { status: 400 })
  }
  
  const buffer = Buffer.from(await file.arrayBuffer())
  await saveFile(buffer, file.name)
  
  return json({ success: true, filename: file.name })
}
```

## Multiple Actions

```typescript
export const action = async ({ request }: ActionFunctionArgs) => {
  const formData = await request.formData()
  const intent = formData.get('intent')
  
  switch (intent) {
    case 'create':
      return createItem(formData)
    case 'update':
      return updateItem(formData)
    case 'delete':
      return deleteItem(formData)
    default:
      return json({ error: 'Invalid intent' }, { status: 400 })
  }
}
```
