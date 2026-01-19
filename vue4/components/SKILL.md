---
name: components
description: >
  Components in Vue 4 with Composition API.
  Trigger: When working with Vue 4 components - script setup, props, emits, slots
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Vue 4 Components"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Components Vue 4

## Component Basic

```vue
<script setup lang="ts">
interface Props {
  title: string
  user?: { id: number; name: string }
  onLogout?: () => void
}

const props = defineProps<Props>()
const emit = defineEmits<{
  (e: 'update', value: string): void
}>()
</script>

<template>
  <header class="app-header">
    <h1>{{ title }}</h1>
    <button v-if="user" @click="emit('update', 'new')">
      {{ user.name }}
    </button>
  </header>
</template>
```

## Script Setup

```vue
<script setup lang="ts">
const count = ref(0)
const doubled = computed(() => count.value * 2)

function increment() {
  count.value++
}
</script>
```

## Props y Emits

```vue
<script setup lang="ts">
// Props con tipos
defineProps<{
  title: string
  count: number
}>()

// Emits tipados
const emit = defineEmits<{
  (e: 'increment'): void
  (e: 'change', value: number): void
}>()
</script>
```

## Slots

```vue
<template>
  <div class="card">
    <slot name="header" />
    <slot />
    <slot name="footer" />
  </div>
</template>
```
