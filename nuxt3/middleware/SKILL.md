---
name: middleware
description: >
  Middleware in Nuxt 3.
  Trigger: When working with Nuxt middleware - route guards, authentication, authorization, redirects
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Nuxt Middleware / Auth"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Nuxt 3 Middleware

## Global Middleware

```typescript
// middleware/auth.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useUser();
  
  if (!user.value && to.path !== '/login') {
    return navigateTo('/login');
  }
});
```

## Route Middleware

```typescript
// middleware/admin.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useUser();
  
  if (!user.value?.isAdmin) {
    return abortNavigation('No autorizado');
  }
});

// Usage in page
definePageMeta({
  middleware: ['admin']
});
```

## Multiple Middleware

```typescript
definePageMeta({
  middleware: ['auth', 'admin']
});
```

## Named Middleware with Options

```typescript
// middleware/redirect.ts
export default defineNuxtRouteMiddleware((to, from) => {
  if (to.path === '/old-path') {
    return navigateTo('/new-path', { redirectCode: 301 });
  }
});
```

## Middleware with Parameters

```typescript
// middleware/role.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const requiredRole = to.meta.role;
  const user = useUser();
  
  if (user.value?.role !== requiredRole) {
    return navigateTo('/unauthorized');
  }
});

// Usage
definePageMeta({
  middleware: {
    name: 'role',
    role: 'admin'
  }
});
```

## Server Middleware

```typescript
// server/middleware/logger.ts
export default defineEventHandler((event) => {
  console.log(`${event.method} ${event.path}`);
});
```
