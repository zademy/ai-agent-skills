---
name: flexbox
description: >
  CSS Flexbox modern.
  Trigger: When working with CSS Flexbox - display: flex, justify-content, align-items, gap, flex properties
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "CSS Flexbox / Layout"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# CSS Flexbox

## Contenedor Flex

```css
.container {
    display: flex;
    flex-direction: row | row-reverse | column | column-reverse;
    justify-content: flex-start | flex-end | center | space-between | space-around;
    align-items: stretch | flex-start | flex-end | center | baseline;
    gap: 1rem;
}
```

## Items Flex

```css
.item {
    flex-grow: 1;
    flex-shrink: 0;
    flex-basis: 200px;
    flex: 1 1 200px;
    align-self: auto | flex-start | flex-end | center;
}
```
