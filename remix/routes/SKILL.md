---
name: routes
description: Routing in Remix
---

# Remix Routes

## File-based Routing

```
app/
├── routes/
│   ├── _index.tsx        # /
│   ├── about.tsx         # /about
│   ├── users.tsx         # /users
│   ├── users.$id.tsx     # /users/:id
│   ├── users.$id.edit.tsx # /users/:id/edit
│   ├── users._index.tsx  # /users (list)
│   ├── users.layout.tsx  # /users (layout wrapper)
│   ├── auth.login.tsx    # /auth/login
│   └── $.tsx             # 404 catch-all
```

## Route Modules

```typescript
// routes/_index.tsx
export default function Index() {
  return <h1>Home Page</h1>
}

// routes/about.tsx
export default function About() {
  return <h1>About Page</h1>
}
```

## Dynamic Segments

```typescript
// routes/users.$id.tsx
import { LoaderFunctionArgs, json } from '@remix-run/node'

export const loader = async ({ params }: LoaderFunctionArgs) => {
  const user = await getUser(params.id)
  return json({ user })
}

export default function UserProfile() {
  const { user } = useLoaderData<typeof loader>()
  return <h1>{user.name}</h1>
}

// URL: /users/123
// params.id = "123"
```

## Nested Routes

```typescript
// routes/dashboard.tsx (layout)
export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="dashboard">
      <nav><DashboardSidebar /></nav>
      <main>{children}</main>
    </div>
  )
}

// routes/dashboard._index.tsx (index)
export default function DashboardIndex() {
  return <h1>Dashboard Home</h1>
}

// routes/dashboard.settings.tsx
export default function DashboardSettings() {
  return <h1>Settings</h1>
}
```

## Optional Segments

```typescript
// routes/files.$.tsx (optional segment)
// Matches: /files, /files/a, /files/a/b

// routes/users.$userId.projects.$projectId.tsx
// Required: both params
```

## Splat Routes (Catch-all)

```typescript
// routes/$.tsx (catch-all)
export default function CatchAll({ params }: { params: { '*'?: string } }) {
  return <p>Not found: {params['*']}</p>
}
```

## Layout Routes

```typescript
// routes/admin.tsx (layout only, no component)
export default function AdminLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="admin">
      <AdminNav />
      {children}
    </div>
  )
}
```

## Resource Routes

```typescript
// routes/api.users.ts (no UI, just data)
export const loader = async () => {
  return json(await getUsers())
}

export const action = async ({ request }: ActionFunctionArgs) => {
  return createUser(await request.json())
}
```

## Route Meta

```typescript
import type { MetaFunction } from '@remix-run/node'

export const meta: MetaFunction = () => {
  return [
    { title: 'Page Title' },
    { name: 'description', content: 'Description' }
  ]
}
```

## Error Boundaries

```typescript
export function ErrorBoundary() {
  const error = useRouteError()
  return (
    <div>
      <h1>Error</h1>
      <p>{error instanceof Error ? error.message : 'Unknown error'}</p>
    </div>
  )
}
```
