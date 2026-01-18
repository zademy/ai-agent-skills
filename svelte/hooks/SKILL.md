---
name: hooks
description: Hooks and lifecycle in Svelte 5 with runes
---

# Hooks Svelte 5

## Lifecycle Functions

```svelte
<script lang="ts">
  import { onMount, onDestroy } from 'svelte'

  let data = $state(null)

  onMount(async () => {
    const response = await fetch('/api/data')
    data = await response.json()
    
    console.log('Component mounted')
  })

  onDestroy(() => {
    console.log('Component destroyed')
    // Cleanup
  })
</script>

{#if data}
  <p>{data}</p>
{/if}
```

## $effect

```svelte
<script lang="ts">
  let count = $state(0)
  let doubled = $derived(count * 2)

  $effect(() => {
    console.log(`Count: ${count}, Doubled: ${doubled}`)
    
    // Cleanup function
    return () => {
      console.log('Effect cleaned up')
    }
  })
</script>

<button onclick={() => count++}>Increment</button>
```

## $state y $derived

```svelte
<script lang="ts">
  let user = $state({ name: 'John', age: 30 })
  let isAdult = $derived(user.age >= 18)
  
  function updateName(name: string) {
    user.name = name
  }
</script>

<h1>{user.name} ({isAdult ? 'Adult' : 'Minor'})</h1>
```

## $props

```svelte
<script lang="ts">
  interface Props {
    title: string
    value?: number
    onincrement?: () => void
  }

  let { title, value = 0, onincrement }: Props = $props()
</script>

<h1>{title}</h1>
<button onclick={onincrement}>+</button>
```

## $props con默认值

```svelte
<script lang="ts">
  let {
    title = 'Default Title',
    count = 0,
    items = []
  }: {
    title?: string
    count?: number
    items?: string[]
  } = $props()
</script>
```
