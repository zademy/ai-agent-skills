---
name: pages
description: Pages in Astro 4 with static and server rendering
---

# Páginas Astro 4

## Page Basic

```astro
---
// Frontmatter (Server-side)
import { getData } from '../lib/data'

const data = await getData()
---

<html lang="es">
  <head>
    <title>Astro Page</title>
  </head>
  <body>
    <h1>Bienvenido</h1>
    <ul>
      {data.map(item => (
        <li>{item.name}</li>
      ))}
    </ul>
  </body>
</html>
```

## Dynamic Routes

```
src/
└── pages/
    ├── index.astro
    └── users/
        ├── index.astro
        └── [id].astro
```

```astro
---
// src/pages/users/[id].astro
import { getUser } from '../../lib/users'

const { id } = Astro.params
const user = await getUser(id)

if (!user) {
  return Astro.redirect('/404')
}
---

<h1>{user.name}</h1>
<p>{user.email}</p>
```

## Static Generation

```astro
---
export async function getStaticPaths() {
  const users = await fetch('https://api.example.com/users').then(r => r.json())
  
  return users.map(user => ({
    params: { id: user.id },
    props: { user }
  }))
}

const { user } = Astro.props
---

<h1>{user.name}</h1>
```

## Server Mode

```astro
---
// Server-side rendering
export const prerender = false

const response = await fetch(Astro.url)
const data = await response.json()
---

<p>{data.message}</p>
```
