---
name: composables
description: Composables in Vue 4 with Composition API
---

# Composables Vue 4

## useCounter

```typescript
export function useCounter(initial = 0) {
  const count = ref(initial)
  
  const increment = () => count.value++
  const decrement = () => count.value--
  const reset = () => count.value = initial
  
  return {
    count: readonly(count),
    increment,
    decrement,
    reset
  }
}
```

## useFetch

```typescript
export function useFetch<T>(url: string) {
  const data = ref<T | null>(null)
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
  
  onMounted(fetchData)
  
  return { data, error, pending, refresh: fetchData }
}
```

## useLocalStorage

```typescript
export function useLocalStorage<T>(key: string, defaultValue: T) {
  const storedValue = ref<T>(defaultValue)
  
  if (process.client) {
    const item = localStorage.getItem(key)
    if (item) {
      try {
        storedValue.value = JSON.parse(item)
      } catch {
        storedValue.value = item as unknown as T
      }
    }
  }
  
  watch(storedValue, (newValue) => {
    if (process.client) {
      localStorage.setItem(key, JSON.stringify(newValue))
    }
  }, { deep: true })
  
  return storedValue
}
```

## useDebounce

```typescript
export function useDebounce<T>(value: Ref<T>, delay = 300) {
  const debouncedValue = ref(value.value) as Ref<T>
  
  let timeout: ReturnType<typeof setTimeout>
  
  watch(value, (newValue) => {
    clearTimeout(timeout)
    timeout = setTimeout(() => {
      debouncedValue.value = newValue
    }, delay)
  })
  
  return debouncedValue
}
```
