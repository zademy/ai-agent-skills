---
name: composables
description: >
  Composables in Nuxt 4.
  Trigger: When working with Nuxt 4 composables - useState, custom hooks, data fetching
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Nuxt 4 Composables / State"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Composables Nuxt 4

## useCounter

```typescript
export const useCounter = () => {
  const count = useState('count', () => 0)
  
  const increment = () => count.value++
  const decrement = () => count.value--
  const reset = () => count.value = 0
  
  return { count: readonly(count), increment, decrement, reset }
}
```

## useApi

```typescript
export const useApi = <T>(url: string) => {
  const data = useState<T | null>(`api-${url}`, () => null)
  const error = ref<Error | null>(null)
  const pending = ref(false)
  
  const fetchData = async () => {
    pending.value = true
    try {
      data.value = await $fetch<T>(url)
    } catch (e) {
      error.value = e instanceof Error ? e : new Error(String(e))
    } finally {
      pending.value = false
    }
  }
  
  return { data, error, pending, refresh: fetchData }
}
```
