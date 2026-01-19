---
name: basics
description: >
  Astro basics.
  Trigger: When working with Astro - components, layouts, props, slots, SSG, SSR
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Astro / Static Site"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Astro Basics

## Project Structure

```
src/
├── pages/
│   ├── index.astro
│   └── about.astro
├── components/
│   └── Header.astro
├── layouts/
│   └── Layout.astro
└── content/
    └── blog/
        └── post-1.md
```

## Basic Component

```astro
---
// Frontmatter (Server-side)
const title = 'Hello World'
const user = { name: 'John', age: 30 }
---

<html lang="en">
  <head>
    <title>{title}</title>
  </head>
  <body>
    <h1>{title}</h1>
    <p>Hello {user.name}!</p>
    
    <!-- JSX-like syntax -->
    <ul>
      {user.name && <li>User exists</li>}
    </ul>
    
    <!-- Server-only comments -->
    {/* This is also server-only */}
  </body>
</html>

<style>
  h1 {
    color: red;
  }
</style>
```

## Props

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

<!-- Usage -->
<Card title="My Card" description="Custom desc">
  <p>Card content</p>
</Card>
```

## Slots

```astro
---
// Layout.astro
const { title } = Astro.props
---

<html>
  <head><title>{title}</title></head>
  <body>
    <header><slot name="header" /></header>
    <main><slot /></main>
    <footer><slot name="footer" /></footer>
  </body>
</html>

<!-- Usage -->
<Layout title="Page Title">
  <h1 slot="header">Header</h1>
  <p>Main content</p>
  <p slot="footer">Footer</p>
</Layout>
```

## Server-Side vs Client-Side

```astro
---
// This runs at build time (SSG) or server (SSR)
const data = await fetch('https://api.example.com/data').then(r => r.json())
---

<h1>{data.title}</h1>

<!-- Client-side with hydration -->
<script>
  // This runs in the browser
  console.log('Hello from browser')
</script>

<!-- Client directive -->
<Counter client:load />      <!-- Load immediately -->
<Counter client:idle />      <!-- Load when browser idle -->
<Counter client:visible />   <!-- Load when visible -->
<Counter client:media />     <!-- Load when media query matches -->
```

## Imports

```astro
---
// Import components
import Header from '../components/Header.astro'
import Footer from '../components/Footer.astro'

// Import markdown/content
import { getCollection } from 'astro:content'

// Import images
import myImage from '../images/logo.png'
---

<img src={myImage.src} alt="Logo" />
```

## Dynamic Routes

```astro
---
// pages/blog/[slug].astro
import { getCollection } from 'astro:content'

export async function getStaticPaths() {
  const posts = await getCollection('blog')
  return posts.map(post => ({
    params: { slug: post.slug },
    props: { post }
  }))
}

const { post } = Astro.props
const { Content } = await post.render()
---

<article>
  <h1>{post.data.title}</h1>
  <Content />
</article>
```
