---
name: components
description: >
  Components in Nuxt 3 and 4 with auto-import.
  Trigger: When working with Nuxt components - auto-import, props, emits, nested components
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Nuxt Components"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
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
