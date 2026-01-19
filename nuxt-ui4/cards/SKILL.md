---
name: cards
description: >
  Cards in Nuxt UI v4.
  Trigger: When working with cards - UCard, variants, slots, headers, footers, actions
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Nuxt UI Cards / Containers"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Nuxt UI v4 Cards

## Basic Card

```vue
<script setup lang="ts">
const user = { name: 'John', email: 'john@email.com' }
</script>

<template>
  <UCard>
    <template #header>
      <h3 class="text-lg font-semibold">User Profile</h3>
    </template>
    
    <p>Name: {{ user.name }}</p>
    <p>Email: {{ user.email }}</p>
    
    <template #footer>
      <UButton>Edit Profile</UButton>
    </template>
  </UCard>
</template>
```

## Card with Actions

```vue
<template>
  <UCard>
    <template #header>
      <div class="flex justify-between items-center">
        <h3 class="text-lg font-semibold">Project A</h3>
        <UBadge color="green">Active</UBadge>
      </div>
    </template>
    
    <p class="text-gray-600">Description of the project goes here.</p>
    
    <template #footer>
      <div class="flex gap-2">
        <UButton size="sm" variant="soft">View Details</UButton>
        <UButton size="sm" color="red" variant="soft">Delete</UButton>
      </div>
    </template>
  </UCard>
</template>
```

## Card Variations

```vue
<!-- Elevated (default) -->
<UCard variant="elevated">

<!-- Subtle -->
<UCard variant="subtle">

<!-- Outline -->
<UCard variant="outline">

<!-- Soft -->
<UCard variant="soft">
```

## Card with Complex Content

```vue
<template>
  <UCard class="w-full max-w-md">
    <template #header>
      <div class="flex items-center gap-3">
        <UAvatar src="https://example.com/avatar.jpg" alt="User" />
        <div>
          <h3 class="text-sm font-semibold">Jane Smith</h3>
          <p class="text-xs text-gray-500">Software Engineer</p>
        </div>
      </div>
    </template>
    
    <div class="space-y-2">
      <div class="flex justify-between text-sm">
        <span class="text-gray-500">Projects</span>
        <span class="font-medium">12</span>
      </div>
      <div class="flex justify-between text-sm">
        <span class="text-gray-500">Tasks</span>
        <span class="font-medium">45</span>
      </div>
    </div>
    
    <template #footer>
      <UProgress :value="75" size="xs" />
    </template>
  </UCard>
</template>
```

## Card Grid Layout

```vue
<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
    <UCard v-for="item in items" :key="item.id">
      <template #header>
        {{ item.title }}
      </template>
      {{ item.description }}
    </UCard>
  </div>
</template>
```
