---
name: loaders
description: Loaders in Remix
---

# Remix Loaders

## Basic Loader

```typescript
import { json } from '@remix-run/node'
import { useLoaderData } from '@remix-run/react'

export const loader = async () => {
  const users = await db.user.findMany()
  return json({ users })
}

export default function UsersPage() {
  const { users } = useLoaderData<typeof loader>()
  
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  )
}
```

## Loader with Params

```typescript
import { json, LoaderFunctionArgs } from '@remix-run/node'

export const loader = async ({ params }: LoaderFunctionArgs) => {
  const user = await db.user.findUnique({
    where: { id: params.userId }
  })
  
  if (!user) {
    throw new Response('Not Found', { status: 404 })
  }
  
  return json({ user })
}
```

## Loader with Query Params

```typescript
export const loader = async ({ request }: LoaderFunctionArgs) => {
  const url = new URL(request.url)
  const search = url.searchParams.get('search')
  const status = url.searchParams.get('status')
  
  const posts = await db.post.findMany({
    where: {
      title: search ? { contains: search } : undefined,
      status: status || undefined
    }
  })
  
  return json({ posts })
}
```

## Defer Streaming

```typescript
import { defer, LoaderFunctionArgs } from '@remix-run/node'

export const loader = async ({ request }: LoaderFunctionArgs) => {
  const user = await getUser(request)
  const reviews = getReviews(user.id) // Promise
  
  return defer({
    user,
    reviews: await reviews // Await for critical data
  })
}

export default function UserPage() {
  const { user, reviews } = useLoaderData<typeof loader>()
  const reviewsDeferred = useMatchesData('routes/user.$id')
  
  return (
    <div>
      <h1>{user.name}</h1>
      <Suspense fallback={<ReviewsSkeleton />}>
        <Await resolve={reviewsDeferred?.reviews}>
          {(reviews) => <ReviewsList reviews={reviews} />}
        </Await>
      </Suspense>
    </div>
  )
}
```

## Error Handling in Loader

```typescript
export const loader = async ({ params }: LoaderFunctionArgs) => {
  try {
    const data = await getData(params.id)
    return json({ data })
  } catch (error) {
    throw new Response('Error loading data', { status: 500 })
  }
}

export function ErrorBoundary() {
  const error = useRouteError()
  return <div>Error: {error.message}</div>
}
```

## Cookie Session

```typescript
import { createCookieSessionStorage } from '@remix-run/node'

const sessionStorage = createCookieSessionStorage({
  cookie: {
    name: '_session',
    sameSite: 'lax',
    path: '/',
    httpOnly: true,
    secrets: ['s3cr3t'],
    secure: process.env.NODE_ENV === 'production'
  }
})

export const loader = async ({ request }: LoaderFunctionArgs) => {
  const session = await sessionStorage.getSession(request.headers.get('Cookie'))
  const userId = session.get('userId')
  
  return json({ userId })
}

export const action = async ({ request }: ActionFunctionArgs) => {
  const session = await sessionStorage.getSession(request.headers.get('Cookie'))
  session.set('userId', '123')
  
  return json(null, {
    headers: { 'Set-Cookie': await sessionStorage.commitSession(session) }
  })
}
```
