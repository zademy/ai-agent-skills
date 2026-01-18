---
name: grid
description: Grid system in Bootstrap 5 with 12 columns
---

# Grid Bootstrap 5

## Sistema de 12 Columnas

```html
<div class="container">
  <div class="row">
    <div class="col-12 col-md-6 col-lg-4">
      <div class="card">Columna 1</div>
    </div>
    <div class="col-12 col-md-6 col-lg-4">
      <div class="card">Columna 2</div>
    </div>
    <div class="col-12 col-md-12 col-lg-4">
      <div class="card">Columna 3</div>
    </div>
  </div>
</div>
```

## Breakpoints

| Breakpoint | Prefijo | Dimension |
|------------|---------|-----------|
| X-Small | `col-` | <576px |
| Small | `col-sm-` | ≥576px |
| Medium | `col-md-` | ≥768px |
| Large | `col-lg-` | ≥992px |
| X-Large | `col-xl-` | ≥1200px |
| XX-Large | `col-xxl-` | ≥1400px |

## Ejemplos

```html
<!-- 2 columnas iguales en tablet, 4 en desktop -->
<div class="row">
  <div class="col-6 col-lg-3">Item 1</div>
  <div class="col-6 col-lg-3">Item 2</div>
  <div class="col-6 col-lg-3">Item 3</div>
  <div class="col-6 col-lg-3">Item 4</div>
</div>

<!-- Offset -->
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4 ms-auto">.col-md-4 .ms-auto</div>
</div>

<!-- Gutter -->
<div class="row g-4">
  <div class="col-md-6">Con gap</div>
  <div class="col-md-6">Con gap</div>
</div>
```
