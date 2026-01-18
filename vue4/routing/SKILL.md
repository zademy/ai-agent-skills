---
name: routing
description: Routing in Vue 4 with Vue Router 4
---

# Routing Vue 4

## Router Setup

```typescript
// router/index.ts
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    },
    {
      path: '/about',
      name: 'about',
      component: () => import('../views/AboutView.vue')
    },
    {
      path: '/users/:id',
      name: 'user',
      component: () => import('../views/UserView.vue'),
      props: true
    }
  ]
})

export default router
```

## Navigation

```vue
<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()

// Navegación programática
router.push('/about')
router.push({ name: 'user', params: { id: '123' } })
router.replace('/home')
router.back()

// Obtener parámetros
const id = route.params.id
const query = route.query.page
</script>

<template>
  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/about">About</RouterLink>
    <RouterLink :to="'/users/' + userId">User</RouterLink>
  </nav>
  <RouterView />
</template>
```

## Route Guards

```typescript
router.beforeEach((to, from, next) => {
  const isAuthenticated = // lógica de autenticación
  if (to.meta.requiresAuth && !isAuthenticated) {
    next('/login')
  } else {
    next()
  }
})
```
