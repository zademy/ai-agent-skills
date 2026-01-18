---
name: basics
description: Fundamentals of Tailwind CSS
---

# Tailwind CSS Basics

## Instalación

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## Configuración

```javascript
// tailwind.config.js
module.exports = {
  content: [
    './src/**/*.{html,js,jsx,ts,tsx,vue}',
  ],
  theme: {
    extend: {
      colors: {
        primary: '#1d4ed8',
        secondary: '#64748b',
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
      },
    },
  },
  plugins: [],
}
```

## Utility Classes

```html
<!-- Layout -->
<div class="flex flex-row gap-4 p-6 m-4">
  <div class="w-1/3">Column 1</div>
  <div class="w-1/3">Column 2</div>
  <div class="w-1/3">Column 3</div>
</div>

<!-- Typography -->
<h1 class="text-4xl font-bold text-gray-900 mb-4">Title</h1>
<p class="text-lg text-gray-600 leading-relaxed">Description</p>

<!-- Spacing -->
<div class="p-4 m-2 space-y-4">
  <div class="px-3 py-2">Item 1</div>
  <div class="px-3 py-2">Item 2</div>
</div>

<!-- Colors -->
<button class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded">
  Button
</button>

<!-- Responsive -->
<div class="w-full md:w-1/2 lg:w-1/3">
  Responsive width
</div>
```
