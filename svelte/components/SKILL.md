---
name: components
description: Components in Svelte
---

# Svelte Components

## Basic Component

```svelte
<script>
  export let name = 'World'
  export let count = 0
  
  function handleClick() {
    count += 1
  }
</script>

<div class="greeting">
  <h1>Hello {name}!</h1>
  <p>Count: {count}</p>
  <button on:click={handleClick}>Increment</button>
</div>

<style>
  .greeting {
    padding: 1rem;
  }
</style>
```

## Component Props

```svelte
<!-- Card.svelte -->
<script>
  export let title: string
  export let description: string = ''
  export let variant: 'primary' | 'secondary' | 'danger' = 'primary'
</script>

<div class="card {variant}">
  <h2>{title}</h2>
  {#if description}
    <p>{description}</p>
  {/if}
  <slot />
</div>

<style>
  .card {
    padding: 1rem;
    border-radius: 8px;
  }
  .primary { background: blue; }
  .secondary { background: gray; }
  .danger { background: red; }
</style>

<!-- Usage -->
<Card title="Hello" description="World" variant="primary" />
```

## Slot

```svelte
<!-- Modal.svelte -->
<script>
  export let open = false
</script>

{#if open}
  <div class="modal">
    <div class="content">
      <slot />
    </div>
  </div>
{/if}

<style>
  .modal {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.5);
  }
  .content {
    background: white;
    padding: 2rem;
  }
</style>

<!-- Usage -->
<Modal open={true}>
  <h2>Title</h2>
  <p>Content</p>
</Modal>
```

## Named Slots

```svelte
<!-- Layout.svelte -->
<div class="layout">
  <header>
    <slot name="header" />
  </header>
  <main>
    <slot />
  </main>
  <footer>
    <slot name="footer" />
  </footer>
</div>

<!-- Usage -->
<Layout>
  <svelte:fragment slot="header">
    <h1>My App</h1>
  </svelte:fragment>
  
  <p>Main content</p>
  
  <svelte:fragment slot="footer">
    <small>Footer</small>
  </svelte:fragment>
</Layout>
```

## Scoped Slots

```svelte
<!-- List.svelte -->
<script>
  export let items: string[]
</script>

<ul>
  {#each items as item}
    <li>
      <slot {item} index={items.indexOf(item)} />
    </li>
  {/each}
</ul>

<!-- Usage -->
<List items={['a', 'b', 'c']} let:item let:index>
  <span>{index}: {item}</span>
</List>
```
