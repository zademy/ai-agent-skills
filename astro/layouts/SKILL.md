---
name: layouts
description: Layouts in Astro
---

# Layouts Astro

## Layout Basic

```astro
---
// src/layouts/BaseLayout.astro
interface Props {
  title: string
}

const { title } = Astro.props
---

<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width" />
    <title>{title}</title>
  </head>
  <body>
    <header>
      <nav>
        <a href="/">Home</a>
        <a href="/about">About</a>
      </nav>
    </header>
    
    <main>
      <slot />
    </main>
    
    <footer>
      <p>&copy; 2024 Mi App</p>
    </footer>
  </body>
</html>
```

## Uso del Layout

```astro
---
// src/pages/index.astro
import BaseLayout from '../layouts/BaseLayout.astro'
---

<BaseLayout title="Home">
  <h1>Bienvenido a mi sitio</h1>
  <p>Contenido  of the página principal.</p>
</BaseLayout>
```

## Named Slots

```astro
<!-- Card.astro -->
<article class="card">
  <header>
    <slot name="header" />
  </header>
  <div class="content">
    <slot />
  </div>
  <footer>
    <slot name="footer" />
  </footer>
</article>

<!-- Uso -->
<Card>
  <h2 slot="header">Título</h2>
  Contenido
  <p slot="footer">Footer</p>
</Card>
```
