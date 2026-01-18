---
name: modals
description: Modals in Nuxt UI v4
---

# Nuxt UI v4 Modals

## Basic Modal

```vue
<script setup lang="ts">
const isOpen = ref(false)

function openModal() {
  isOpen.value = true
}

function closeModal() {
  isOpen.value = false
}
</script>

<template>
  <UButton @click="openModal">Open Modal</UButton>
  
  <UModal v-model="isOpen">
    <UCard>
      <template #header>
        <div class="flex justify-between items-center">
          <h3 class="text-lg font-semibold">Modal Title</h3>
          <UButton
            icon="i-heroicons-x-mark"
            color="gray"
            variant="ghost"
            @click="closeModal"
          />
        </div>
      </template>
      
      <p>Modal content goes here.</p>
      
      <template #footer>
        <div class="flex justify-end gap-2">
          <UButton color="gray" variant="soft" @click="closeModal">
            Cancel
          </UButton>
          <UButton @click="handleSave">Save</UButton>
        </div>
      </template>
    </UCard>
  </UModal>
</template>
```

## Modal with Form

```vue
<script setup lang="ts">
const form = reactive({
  name: '',
  email: ''
})

const isOpen = ref(false)

async function submitForm() {
  // Handle form submission
  await submit(form)
  isOpen.value = false
}
</script>

<template>
  <UModal v-model="isOpen">
    <UCard>
      <template #header>
        <h3 class="text-lg font-semibold">Create User</h3>
      </template>
      
      <UForm :state="form" class="space-y-4">
        <UFormGroup label="Name">
          <UInput v-model="form.name" />
        </UFormGroup>
        
        <UFormGroup label="Email">
          <UInput v-model="form.email" type="email" />
        </UFormGroup>
      </UForm>
      
      <template #footer>
        <div class="flex justify-end gap-2">
          <UButton color="gray" variant="soft" @click="isOpen = false">
            Cancel
          </UButton>
          <UButton @click="submitForm">Create</UButton>
        </div>
      </template>
    </UCard>
  </UModal>
</template>
```

## Modal Size Variations

```vue
<!-- Small -->
<UModal size="xs">

<!-- Medium (default) -->
<UModal size="sm">

<!-- Large -->
<UModal size="lg">

<!-- Extra large -->
<UModal size="xl">

<!-- Full screen -->
<UModal fullscreen>
```

## Modal with Confirm

```vue
<script setup lang="ts">
const isOpen = ref(false)

async function confirmDelete() {
  const confirmed = await confirm({
    title: 'Delete Item',
    description: 'Are you sure you want to delete this item?',
    confirmText: 'Delete',
    cancelText: 'Cancel',
    type: 'error'
  })
  
  if (confirmed) {
    // Delete logic
  }
}
</script>
```

## Modal with Overlay Close

```vue
<UModal
  v-model="isOpen"
  :close="{ onClick: closeModal }"
  :ui="{
    overlay: 'fixed inset-0 bg-black/50',
    base: 'relative z-50'
  }"
>
```
