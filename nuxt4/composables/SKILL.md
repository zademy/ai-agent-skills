---
name: composables
description: Composables in Nuxt 4
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
