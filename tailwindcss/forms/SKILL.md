---
name: forms
description: Forms with Tailwind CSS
---

# Tailwind CSS Forms

## Input

```html
<input
  type="text"
  class="
    w-full
    px-4 py-2
    border border-gray-300
    rounded-lg
    focus:outline-none focus:ring-2 focus:ring-blue-500
    disabled:bg-gray-100 disabled:cursor-not-allowed
  "
  placeholder="Enter text"
/>
```

## Textarea

```html
<textarea
  class="
    w-full
    px-4 py-2
    border border-gray-300
    rounded-lg
    focus:outline-none focus:ring-2 focus:ring-blue-500
    resize-none
  "
  rows="4"
></textarea>
```

## Select

```html
<select
  class="
    w-full
    px-4 py-2
    border border-gray-300
    rounded-lg
    bg-white
    focus:outline-none focus:ring-2 focus:ring-blue-500
  "
>
  <option>Option 1</option>
  <option>Option 2</option>
</select>
```

## Checkbox

```html
<label class="flex items-center gap-2 cursor-pointer">
  <input
    type="checkbox"
    class="
      w-5 h-5
      text-blue-600
      border-gray-300 rounded
      focus:ring-blue-500
    "
  />
  <span>Checkbox label</span>
</label>
```

## Radio

```html
<label class="flex items-center gap-2 cursor-pointer">
  <input
    type="radio"
    name="radio-group"
    class="w-5 h-5 text-blue-600 border-gray-300 focus:ring-blue-500"
  />
  <span>Radio label</span>
</label>
```

## Switch Toggle

```html
<label class="relative inline-flex items-center cursor-pointer">
  <input type="checkbox" class="sr-only peer" />
  <div class="
    w-11 h-6
    bg-gray-200
    peer-focus:outline-none peer-focus:ring-4
    peer-focus:ring-blue-300
    rounded-full peer
    peer-checked:after:translate-x-full
    peer-checked:after:border-white
    after:content-['']
    after:absolute after:top-[2px] after:left-[2px]
    after:bg-white after:border-gray-300 after:border
    after:rounded-full after:h-5 after:w-5
    after:transition-all
    peer-checked:bg-blue-600
  "></div>
  <span class="ml-3">Toggle</span>
</label>
```

## Form Group with Label

```html
<div class="space-y-2">
  <label for="email" class="block text-sm font-medium text-gray-700">
    Email
  </label>
  <input
    id="email"
    type="email"
    class="
      w-full
      px-4 py-2
      border border-gray-300
      rounded-lg
      focus:ring-2 focus:ring-blue-500 focus:border-blue-500
    "
  />
</div>
```

## Error State

```html
<div class="space-y-2">
  <label class="block text-sm font-medium text-gray-700">
    Email
  </label>
  <input
    type="email"
    class="
      w-full
      px-4 py-2
      border border-red-500
      rounded-lg
      focus:ring-2 focus:ring-red-500 focus:border-red-500
    "
  />
  <p class="text-sm text-red-500">Email is required</p>
</div>
```

## Floating Label

```html
<div class="relative">
  <input
    type="email"
    id="email"
    class="
      peer w-full px-4 py-3
      border border-gray-300
      rounded-lg
      placeholder-transparent
      focus:outline-none focus:ring-2 focus:ring-blue-500
    "
    placeholder="Email"
  />
  <label
    for="email"
    class="
      absolute left-4 top-3
      text-gray-500
      transition-all
      peer-placeholder-shown:text-base
      peer-placeholder-shown:top-3
      peer-focus:-top-2.5
      peer-focus:text-sm
      peer-focus:bg-white peer-focus:px-1
      peer-focus:text-blue-500
    "
  >
    Email
  </label>
</div>
```

## Inline Form

```html
<form class="flex items-end gap-4">
  <div class="flex-1">
    <label class="block text-sm text-gray-700 mb-1">Email</label>
    <input type="email" class="w-full px-3 py-2 border rounded-lg" />
  </div>
  <button class="px-4 py-2 bg-blue-500 text-white rounded-lg">
    Subscribe
  </button>
</form>
```
