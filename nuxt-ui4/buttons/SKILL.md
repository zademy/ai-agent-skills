---
name: buttons
description: UButton in Nuxt UI 4
---

# UButton Nuxt UI 4

## Variantes

```vue
<UButton color="primary">Primary</UButton>
<UButton color="secondary">Secondary</UButton>
<UButton color="success">Success</UButton>
<UButton color="warning">Warning</UButton>
<UButton color="error">Error</UButton>
```

## Tamaños

```vue
<UButton size="xs">Extra Small</UButton>
<UButton size="sm">Small</UButton>
<UButton size="md">Medium</UButton>
<UButton size="lg">Large</UButton>
```

## Estados

```vue
<UButton loading>Cargando</UButton>
<UButton disabled>Deshabilitado</UButton>
<UButton block>Block</UButton>

<UButton variant="solid">Solid</UButton>
<UButton variant="outline">Outline</UButton>
<UButton variant="soft">Soft</UButton>
<UButton variant="ghost">Ghost</UButton>
```

## Con Iconos

```vue
<UButton icon="i-heroicons-plus">Agregar</UButton>
<UButton>
  <template #leading><UIcon name="i-heroicons-user" /></template>
  Perfil
</UButton>
```
