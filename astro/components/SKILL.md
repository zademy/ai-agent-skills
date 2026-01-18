---
name: components
description: Components in Astro
---

# Astro Components

## Basic Component

```astro
---
// Card.astro
interface Props {
  title: string
  description?: string
}

const { title, description = 'Default description' } = Astro.props
---

<div class="card">
  <h2>{title}</h2>
  <p>{description}</p>
  <slot />
</div>

<style>
  .card {
    padding: 1rem;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
  }
</style>
```

## Component with Props

```astro
---
// Button.astro
interface Props {
  variant?: 'primary' | 'secondary' | 'danger'
  size?: 'sm' | 'md' | 'lg'
  disabled?: boolean
}

const {
  variant = 'primary',
  size = 'md',
  disabled = false
} = Astro.props

const classes = `btn btn-${variant} btn-${size}`
---

<button class={classes} disabled={disabled}>
  <slot />
</button>

<style>
  .btn { padding: 0.5rem 1rem; border-radius: 4px; }
  .btn-primary { background: blue; color: white; }
  .btn-secondary { background: gray; color: white; }
  .btn-danger { background: red; color: white; }
  .btn-sm { font-size: 0.875rem; }
  .btn-lg { font-size: 1.25rem; }
</style>
```

## Named Slots

```astro
---
// Modal.astro
interface Props {
  open: boolean
}

const { open } = Astro.props
---

{#if open}
  <div class="modal-overlay">
    <div class="modal">
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
  </div>
{/if}

<style>
  .modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    min-width: 300px;
  }
</style>

<!-- Usage -->
<Modal open={true}>
  <h1 slot="header">Title</h1>
  <p>Content here</p>
  <button slot="footer">Close</button>
</Modal>
```

## Scoped Slots

```astro
---
// List.astro
interface Props {
  items: string[]
}

const { items } = Astro.props
---

<ul>
  {items.map((item, index) => (
    <li>
      <slot item={item} index={index} />
    </li>
  ))}
</ul>

<!-- Usage -->
<List items={['a', 'b', 'c']} let:item let:index>
  <span>{index}: {item}</span>
</List>
```

## Component with Events

```astro
---
// Counter.astro
import { useState } from 'preact/hooks'

const initial = 0
const [count, setCount] = useState(initial)
---

<div class="counter">
  <button onClick={() => setCount(count - 1)}>-</button>
  <span>{count}</span>
  <button onClick={() => setCount(count + 1)}>+</button>
</div>

<style>
  .counter { display: flex; gap: 0.5rem; align-items: center; }
  button { padding: 0.25rem 0.75rem; }
</style>
```
