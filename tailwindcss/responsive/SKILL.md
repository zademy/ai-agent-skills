---
name: responsive
description: Responsive Design with Tailwind CSS
---

# Tailwind CSS Responsive

## Breakpoints

```html
<!-- Mobile first -->
<div class="text-sm md:text-base lg:text-lg">
  Responsive text
</div>

<!-- Breakpoints -->
<!-- sm: 640px -->
<!-- md: 768px -->
<!-- lg: 1024px -->
<!-- xl: 1280px -->
<!-- 2xl: 1536px -->
```

## Responsive Utilities

```html
<!-- Width -->
<div class="w-full md:w-1/2 lg:w-1/3"></div>

<!-- Display -->
<div class="block md:hidden">Hide on desktop</div>
<div class="hidden md:block">Show on desktop</div>

<!-- Flex -->
<div class="flex flex-col md:flex-row">
  <div>Item 1</div>
  <div>Item 2</div>
</div>

<!-- Grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
  <div>Item</div>
</div>

<!-- Padding/Margin -->
<div class="p-4 md:p-6 lg:p-8">
  Responsive spacing
</div>

<!-- Text size -->
<p class="text-xs sm:text-sm md:text-base lg:text-lg">
  Responsive text
</p>
```

## Custom Breakpoints

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    screens: {
      'tablet': '640px',
      'laptop': '1024px',
      'desktop': '1280px',
    }
  }
}
```

```html
<div class="text-base tablet:text-lg laptop:text-xl">
  Custom breakpoints
</div>
```

## Responsive with hover/focus

```html
<button class="
  bg-blue-500 hover:bg-blue-600
  md:bg-green-500 md:hover:bg-green-600
">
  Responsive button
</button>
```

## Only and greater than

```html
<!-- min-width (default) -->
<div class="md:block"> md: 768px and up </div>

<!-- max-width -->
<div class="max-md:hidden"> below 768px </div>

<!-- Between -->
<div class="md:max-lg:bg-blue">
  Between 768px and 1024px
</div>
```

## Column helpers

```html
<!-- All columns responsive -->
<div class="col-span-1 md:col-span-2 lg:col-span-3">
  Responsive column span
</div>

<!-- Start/End -->
<div class="col-start-1 col-end-3 md:col-start-2 md:col-end-4">
  Responsive column position
</div>
```
