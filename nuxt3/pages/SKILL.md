---
name: pages
description: Pages system in Nuxt 3 and Nuxt 4
---

# Páginas en Nuxt 3/4

## Page Basic

```vue
<script setup lang="ts">
const { data: users } = await useFetch('/api/users')
</script>

<template>
  <div>
    <h1>Usuarios</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.name }}
      </li>
    </ul>
  </div>
</template>
```

## Dynamic Routes

```
pages/
├── users/
│   ├── index.vue      # /users
│   └── [id].vue       # /users/:id
└── products/
    ├── [category]/
    │   └── [id].vue   # /products/:category/:id
```

```vue
<script setup lang="ts">
const route = useRoute()
const userId = route.params.id

const { data: user } = await useFetch(`/api/users/${userId}`)
</script>

<template>
  <div v-if="user">
    <h1>{{ user.name }}</h1>
    <p>{{ user.email }}</p>
  </div>
</template>
```

## Nuxt 4 Features (2025)

```vue
<script setup lang="ts">
// Nuxt 4 tiene mejor soporte para async/await
const { data } = await useAsyncData('key', () => fetchData())

// Type safety mejorado
definePageMeta({
  layout: 'default',
  middleware: ['auth']
})
</script>

<template>
  <NuxtPage />
</template>
```

## Nested Pages

```vue
<!-- pages/users/[id].vue -->
<template>
  <div>
    <h1>Usuario {{ $route.params.id }}</h1>
    <NuxtPage />
  </div>
</template>
```
