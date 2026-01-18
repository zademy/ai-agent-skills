---
name: flexbox
description: CSS Flexbox modern
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
