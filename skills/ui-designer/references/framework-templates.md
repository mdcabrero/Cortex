# Framework Templates & Conventions

## Table of Contents
- [Vue 3 (Composition API)](#vue-3-composition-api)
- [Astro](#astro)
- [Plain HTML + Tailwind](#plain-html--tailwind)

---

## Vue 3 (Composition API)

```vue
<script setup>
/**
 * ComponentName
 * Brief description.
 */

// Content data
const heading = 'Exact heading from screenshot'
const description = 'Exact description text.'

// Repeated items
const items = [
  { id: 'item-1', title: 'First Item', text: 'Description' },
  { id: 'item-2', title: 'Second Item', text: 'Description' },
]

// Images — use the image directory identified in Phase 0
const heroImage = '/path/to/project-images/placeholder.jpg'
</script>

<template>
  <section>
    <div class="mx-auto max-w-7xl px-4 md:px-6 lg:px-8">
      <h2 class="text-3xl font-semibold text-foreground md:text-5xl">
        {{ heading }}
      </h2>
      <p class="mt-4 text-muted-foreground lg:text-lg">
        {{ description }}
      </p>

      <div class="mt-8 grid gap-6 md:grid-cols-2 lg:grid-cols-3">
        <div
          v-for="item in items"
          :key="item.id"
          class="rounded-xl border border-border bg-card p-6"
        >
          <h3 class="text-lg font-semibold text-foreground">{{ item.title }}</h3>
          <p class="mt-2 text-muted-foreground">{{ item.text }}</p>
        </div>
      </div>
    </div>
  </section>
</template>
```

### Vue Conventions
- `<script setup>` always first, then `<template>`. No `<style>` block — Tailwind handles styling.
- Use `v-for` with `:key` for lists
- Use `{{ }}` interpolation for text
- Reactive data with `ref()` / `reactive()` only when state changes are needed
- Props with `defineProps()` if the component receives data from a parent
- All text content as `const` variables in `<script setup>` — zero hardcoded strings in `<template>`

---

## Astro

```astro
---
/**
 * ComponentName
 * Brief description.
 */

const heading = "Exact heading from screenshot";
const description = "Exact description text.";

const items = [
  { id: "item-1", title: "First Item", text: "Description" },
  { id: "item-2", title: "Second Item", text: "Description" },
];

// Use the image directory identified in Phase 0
const heroImage = "/path/to/project-images/placeholder.jpg";
---

<section>
  <div class="mx-auto max-w-7xl px-4 md:px-6 lg:px-8">
    <h2 class="text-3xl font-semibold text-foreground md:text-5xl">
      {heading}
    </h2>
    <p class="mt-4 text-muted-foreground lg:text-lg">
      {description}
    </p>

    <div class="mt-8 grid gap-6 md:grid-cols-2 lg:grid-cols-3">
      {items.map((item) => (
        <div key={item.id} class="rounded-xl border border-border bg-card p-6">
          <h3 class="text-lg font-semibold text-foreground">{item.title}</h3>
          <p class="mt-2 text-muted-foreground">{item.text}</p>
        </div>
      ))}
    </div>
  </div>
</section>
```

### Astro Conventions
- All content in frontmatter (`---` block)
- Use `{variable}` interpolation
- Arrays with `.map()` and `key` prop
- No `<style>` block — Tailwind handles styling
- Interactive behavior via `<script>` tags with vanilla JS (not TypeScript)

---

## Plain HTML + Tailwind

```html
<!--
  ComponentName
  Brief description.
-->

<section>
  <div class="mx-auto max-w-7xl px-4 md:px-6 lg:px-8">
    <h2 class="text-3xl font-semibold text-foreground md:text-5xl">
      Exact heading from screenshot
    </h2>
    <p class="mt-4 text-muted-foreground lg:text-lg">
      Exact description text.
    </p>

    <div class="mt-8 grid gap-6 md:grid-cols-2 lg:grid-cols-3">
      <div class="rounded-xl border border-border bg-card p-6">
        <h3 class="text-lg font-semibold text-foreground">First Item</h3>
        <p class="mt-2 text-muted-foreground">Description</p>
      </div>
      <!-- Repeat for each item -->
    </div>
  </div>
</section>
```

### HTML Conventions
- Content inline (no data abstraction layer)
- Comment blocks for component identification
- Repeated elements written out explicitly
