---
name: components
description: >
  Components in Nuxt 4 with new features.
  Trigger: When working with Nuxt 4 components - TypeScript, auto-import, async components
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Nuxt 4 Components"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Components Nuxt 4

## Component Basic

```vue
<script setup lang="ts">
defineProps<{
  title: string
  user?: User
}>()

const emit = defineEmits<{
  (e: 'logout'): void
}>()
</script>

<template>
  <header class="app-header">
    <h1>{{ title }}</h1>
    <button v-if="user" @click="emit('logout')">Logout</button>
  </header>
</template>
```

## Nuxt 4 Features

- Mejor soporte para TypeScript
- Components auto-importados
- Soporte para async/await nativo
