---
name: components
description: Components in Nuxt 3 and 4 with auto-import
---

# Components Nuxt

## Auto-import

```vue
<!-- components/AppHeader.vue -->
<script setup lang="ts">
defineProps<{
  title: string
}>()

const emit = defineEmits<{
  (e: 'logout'): void
}>()
</script>

<template>
  <header class="app-header">
    <h1>{{ title }}</h1>
    <button @click="emit('logout')">Logout</button>
  </header>
</template>
```

## Uso

```vue
<script setup lang="ts">
const user = ref({ name: 'John' })
</script>

<template>
  <AppHeader title="Mi App" :user="user" @logout="handleLogout" />
</template>
```

## Nested Components

```
components/
├── AppHeader.vue       → <AppHeader />
└── base/
    └── BaseButton.vue  → <BaseButton />
```

```vue
<BaseButton variant="primary" @click="submit">
  Enviar
</BaseButton>
```
