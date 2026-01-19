---
name: forms
description: >
  Forms in Nuxt UI 4 with UForm.
  Trigger: When working with forms - UForm, UFormGroup, UInput, validation, submit handling
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "Nuxt UI Forms"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Forms Nuxt UI 4

## UForm

```vue
<script setup lang="ts">
const form = ref({
  name: '',
  email: '',
  password: ''
})

const validate = (state: typeof form.value) => {
  const errors = []
  if (!state.name) errors.push({ name: 'name', message: 'Requerido' })
  if (!state.email.includes('@')) errors.push({ name: 'email', message: 'Email inválido' })
  return errors
}

const onSubmit = () => {
  console.log('Submitted:', form.value)
}
</script>

<template>
  <UForm :state="form" :validate="validate" @submit="onSubmit">
    <UFormGroup name="name" label="Nombre">
      <UInput v-model="form.name" />
    </UFormGroup>
    
    <UFormGroup name="email" label="Email">
      <UInput v-model="form.email" type="email" />
    </UFormGroup>
    
    <UButton type="submit" block>Enviar</UButton>
  </UForm>
</template>
```

## Components  in formulario

```vue
<UInput v-model="value" placeholder="Input" />
<UTextarea v-model="message" rows="4" />
<USelect v-model="selected" :options="options" />
<UCheckbox v-model="checked" label="Acepto" />
<URadio v-model="option" :options="radioOptions" />
```
