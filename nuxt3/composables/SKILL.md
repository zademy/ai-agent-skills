---
name: composables
description: >
  Composables in Nuxt 3/4 with practical examples.
  Trigger: When working with Nuxt composables - useState, custom composables, useFetch, useAuth
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Nuxt Composables / State"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Composables Nuxt

## useCounter

```ts
export const useCounter = () => {
  const count = useState('count', () => 0)
  
  const increment = () => count.value++
  const decrement = () => count.value--
  const reset = () => count.value = 0
  
  return { count: readonly(count), increment, decrement, reset }
}
```

## useFetch Personalizado

```ts
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
  
  onMounted(fetchData)
  
  return { data, error, pending, refresh: fetchData }
}
```

## useAuth (Supabase)

```ts
export const useAuth = () => {
  const user = useSupabaseUser()
  const client = useSupabaseClient()
  
  const login = async (email: string, password: string) => {
    const { error } = await client.auth.signInWithPassword({ email, password })
    return { error }
  }
  
  const logout = async () => {
    await client.auth.signOut()
    navigateTo('/login')
  }
  
  return { user, login, logout }
}
```
