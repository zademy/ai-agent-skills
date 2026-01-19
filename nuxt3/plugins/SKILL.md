---
name: plugins
description: >
  Plugins in Nuxt 3.
  Trigger: When working with Nuxt plugins - client plugins, server plugins, providing methods, hooks
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [core]
  auto_invoke: "Nuxt Plugins / Extensions"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Nuxt 3 Plugins

## Client-si in plugin

```typescript
// plugins/my-plugin.client.ts
export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.provide('myMethod', (msg: string) => {
    console.log(`Plugin says: ${msg}`);
  });
});

// Usage
const { $myMethod } = useNuxtApp();
$myMethod('Hello from plugin');
```

## Server-si in plugin

```typescript
// plugins/my-plugin.server.ts
export default defineNuxtPlugin((nuxtApp) => {
  console.log('This runs on server only');
});
```

## Universal Plugin

```typescript
// plugins/my-plugin.ts
export default defineNuxtPlugin((nuxtApp) => {
  // Runs on both server and client
  nuxtApp.hook('app:created', () => {
    console.log('App created');
  });
});
```

## Providing State

```typescript
// plugins/state.ts
export default defineNuxtPlugin(() => {
  return {
    provide: {
      globalState: ref('Hello')
    }
  };
});
```

## Plugin with Configuration

```typescript
// plugins/config.ts
export default defineNuxtPlugin((nuxtApp) => {
  const config = useRuntimeConfig();
  
  nuxtApp.provide('apiUrl', config.public.apiUrl);
});
```
