---
name: layouts
description: Layouts in Nuxt 3/4
---

# Layouts Nuxt

## Default Layout

```vue
<script setup lang="ts">
const route = useRoute()
</script>

<template>
  <div class="app-layout">
    <header>
      <nav>
        <NuxtLink to="/">Inicio</NuxtLink>
        <NuxtLink to="/about">Acerca</NuxtLink>
      </nav>
    </header>
    
    <main>
      <slot />
    </main>
    
    <footer>
      <p>&copy; {{ new Date().getFullYear() }} Mi App</p>
    </footer>
  </div>
</template>
```

## Admin Layout

```vue
<template>
  <div class="admin-layout">
    <aside class="sidebar">
      <nav>
        <NuxtLink to="/admin/dashboard">Dashboard</NuxtLink>
        <NuxtLink to="/admin/users">Usuarios</NuxtLink>
      </nav>
    </aside>
    
    <main class="content">
      <slot />
    </main>
  </div>
</template>

<style scoped>
.admin-layout {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  width: 250px;
  background: #1a1a1a;
}

.content {
  flex: 1;
  padding: 2rem;
}
</style>
```

## Uso

```vue
<!-- pages/admin/dashboard.vue -->
<script setup lang="ts">
definePageMeta({
  layout: 'admin'
})
</script>
```
