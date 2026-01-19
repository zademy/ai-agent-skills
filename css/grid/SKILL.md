---
name: grid
description: >
  CSS Grid Layout.
  Trigger: When working with CSS Grid - display: grid, grid-template-columns, areas, responsive grids
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "CSS Grid / Layout"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# CSS Grid

## Basic Grid

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  gap: 10px;
}
```

## Grid con fr

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  gap: 20px;
}
```

## Responsive Grid

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}
```

## Grid Areas

```css
.container {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main main"
    "footer footer footer";
  grid-template-columns: 200px 1fr 1fr;
  grid-template-rows: auto 1fr auto;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```

## Grid con span

```css
.item {
  grid-column: span 2;
  grid-row: span 1;
}
```

## Grid con nombres de líneas

```css
.container {
  display: grid;
  grid-template-columns:
    [start] 100px [middle] 1fr [end];
}
```
