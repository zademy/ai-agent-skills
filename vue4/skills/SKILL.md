---
name: skills
description: >
  Skills in Vue 4 - defineProps, defineEmits, defineSlots, defineModel.
  Trigger: When working with Vue 4 skills - props definition, emits, slots, model binding
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Vue 4 Skills / Macros"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Vue 4 Skills

## Define Props

```vue
<script setup lang="ts">
interface Props {
  title: string
  count?: number
  items?: string[]
}

const props = withDefaults(defineProps<Props>(), {
  count: 0,
  items: () => []
})
</script>

<template>
  <div>
    <h1>{{ title }}</h1>
    <p>Count: {{ count }}</p>
    <ul>
      <li v-for="item in items" :key="item">{{ item }}</li>
    </ul>
  </div>
</template>
```

## Define Emits

```vue
<script setup lang="ts">
const emit = defineEmits<{
  (e: 'update', value: string): void
  (e: 'delete', id: number): void
}>()

function handleClick() {
  emit('update', 'new value')
}
</script>
```

## Define Slots

```vue
<script setup lang="ts">
const slot = useSlot()
</script>

<template>
  <div class="card">
    <header>
      <slot name="header" />
    </header>
    <main>
      <slot />
    </main>
    <footer>
      <slot name="footer" :data="slot?.props" />
    </footer>
  </div>
</template>
```

## Expose

```vue
<script setup lang="ts">
const count = ref(0)

defineExpose({
  count,
  increment: () => count.value++
})
</script>
```

## Model Value<script setup lang="ts">
const model

```vue
 = defineModel<string>()
</script>

<template>
  <input v-model="model" />
</template>
```

## Composables

```typescript
// composables/useCounter.ts
export function useCounter(initial = 0) {
  const count = ref(initial)
  
  function increment() {
    count.value++
  }
  
  function decrement() {
    count.value--
  }
  
  return { count, increment, decrement }
}
```

## Plugin

```typescript
// plugins/my-plugin.ts
export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.provide('myPlugin', {
    greet(name: string) {
      return `Hello ${name}!`
    }
  })
})
```
