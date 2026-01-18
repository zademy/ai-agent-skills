---
name: data-fetching
description: Data fetching in Nuxt 3/4 with useFetch and useAsyncData
---

# Data Fetching Nuxt

## useFetch

```ts
const { data, pending, error, refresh } = await useFetch('/api/users')

// Con opciones
const { data: users } = await useFetch('/api/users', {
  method: 'POST',
  body: { name: 'John' },
  headers: { Authorization: `Bearer ${token}` }
})

// Query parameters
const { data: products } = await useFetch('/api/products', {
  query: { page: 1, limit: 10, category: 'electronics' }
})
```

## useAsyncData

```ts
const { data: user, status } = await useAsyncData(
  'user-profile',
  () => $fetch('/api/user/profile'),
  { watch: [userId] }
)

// Con transform
const { data: processedData } = await useAsyncData(
  'processed',
  () => $fetch('/api/data'),
  {
    transform: (data) => data.map((item: any) => ({
      ...item,
      formatted: new Date(item.date).toLocaleDateString()
    }))
  }
)
```

## Route Rules (Nuxt 3.18+)

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  routeRules: {
    '/api/**': { cors: true },
    '/admin/**': { ssr: false },
    '/dashboard/**': { swr: 3600 }, // Cache por 1 hora
    '/offline': { prerender: true }
  }
})
```
