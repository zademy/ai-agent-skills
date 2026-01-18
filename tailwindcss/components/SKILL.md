---
name: components
description: Components with Tailwind CSS
---

# Components Tailwind CSS

## Botones

```html
<!-- Primary -->
<button class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-lg transition-colors">
  Primary
</button>

<!-- Secondary -->
<button class="bg-gray-200 hover:bg-gray-300 text-gray-800 font-medium py-2 px-4 rounded-lg">
  Secondary
</button>

<!-- Outline -->
<button class="border-2 border-blue-500 text-blue-500 hover:bg-blue-50 font-medium py-2 px-4 rounded-lg">
  Outline
</button>

<!-- Sizes -->
<button class="py-1 px-2 text-sm">Small</button>
<button class="py-2 px-4 text-base">Medium</button>
<button class="py-3 px-6 text-lg">Large</button>
```

## Cards

```html
<div class="bg-white rounded-xl shadow-lg overflow-hidden max-w-sm">
  <img src="image.jpg" alt="Card image" class="w-full h-48 object-cover">
  <div class="p-6">
    <h3 class="text-xl font-bold text-gray-900 mb-2">Card Title</h3>
    <p class="text-gray-600">Card description text here.</p>
    <button class="mt-4 w-full bg-blue-500 text-white py-2 rounded-lg hover:bg-blue-600">
      Action
    </button>
  </div>
</div>
```

## Forms

```html
<input
  type="text"
  class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none"
  placeholder="Enter text..."
/>

<select class="w-full px-4 py-2 border border-gray-300 rounded-lg bg-white">
  <option>Option 1</option>
  <option>Option 2</option>
</select>

<label class="flex items-center gap-2">
  <input type="checkbox" class="w-4 h-4 text-blue-500 rounded">
  <span class="text-gray-700">Checkbox label</span>
</label>
```

## Navigation

```html
<nav class="bg-white shadow-md">
  <div class="max-w-7xl mx-auto px-4">
    <div class="flex justify-between h-16">
      <div class="flex items-center">
        <a href="#" class="text-xl font-bold text-gray-900">Logo</a>
      </div>
      <div class="flex items-center space-x-4">
        <a href="#" class="text-gray-600 hover:text-gray-900">Home</a>
        <a href="#" class="text-gray-600 hover:text-gray-900">About</a>
      </div>
    </div>
  </div>
</nav>
```
