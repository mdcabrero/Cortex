---
name: ui-designer
description: Convert UI screenshots into production-ready components, sections, and UI elements that follow the project's design system. Use this skill whenever the user provides a screenshot or visual reference and wants it recreated as a component for their project. Triggers include: recreate this component, build this section, replicate this UI, convert this screenshot, make this for our site, or any request where the user provides a visual reference and expects a coded implementation that matches the project's design tokens and aesthetic. Also use when the user asks to create UI elements, page sections, layouts, or interface patterns from visual references. This skill applies to any frontend framework — Vue, Astro, React, or plain HTML+Tailwind.
---

# UI Designer

Convert UI screenshots into production-ready components that follow the project's design system and visual identity. Outputs pixel-accurate, responsive, accessible code in the project's tech stack.

---

## Principles

1. **Design system first** — Every color, shadow, radius, and font must come from the project's semantic tokens. Never hardcode values that the design system already provides.
2. **Pixel accuracy** — Match the screenshot's layout, spacing, and proportions as closely as possible. When exact values can't be determined, favor the closest Tailwind utility.
3. **Responsive by default** — Every component works at mobile, tablet, and desktop. Mobile-first, progressive enhancement.
4. **Framework-native** — Output idiomatic code for the project's stack. A Vue component should feel like Vue, not a React component with different syntax.

---

## Phase 0: Project Context

Before any screenshot analysis, gather project context. Do this once per session.

### Read the Design System

Load the project's design system files. These are the source of truth:

```
Read global.css (or the project's main Tailwind theme file)
Read DESIGN_BRIEF.md (or equivalent design documentation)
```

From these files, extract and internalize:
- The complete semantic token set (what `--primary`, `--accent`, `--muted`, etc. actually look like)
- The aesthetic direction and design philosophy
- Typography stack and hierarchy
- Spacing conventions, border radius scale, shadow strategy
- Any aesthetic utility classes available (gradients, grain, glass, glow)
- Do's and Don'ts specific to this design system

If these files are not available, ask the user to provide them or point to their location.

### Detect Tech Stack

Determine the output framework in this priority order:

1. **User specifies it** — always takes precedence
2. **CLAUDE.md at project root** — check for stack/framework declarations
3. **package.json** — infer from dependencies:
   - `vue` → Vue 3 (Composition API with `<script setup>`)
   - `astro` → Astro components
   - `react` / `next` → React (JSX)
   - None of the above → plain HTML + Tailwind
4. **File extensions in the project** — `.vue`, `.astro`, `.jsx`/`.tsx`
5. **Ask the user** — if still ambiguous

### Locate Placeholder Images

Check `/src/graphics/` for available placeholder images. Use only what exists:

```
List contents of /src/graphics/
```

Common placeholders: `placeholder.jpg`, `placeholder2.png`, `placeholder3.jpg`, etc.

**Rules:**
- NEVER invent image filenames — only use files that actually exist in the project
- If a component needs multiple images of the same type, cycle through available placeholders
- When no suitable placeholder exists, use a comment: `<!-- Replace: [description of needed image] -->`

---

## Phase 1: Screenshot Analysis

Examine the screenshot with precision. Extract observations in this order:

### 1.1 Text Inventory

List ALL visible text exactly as written. Do not paraphrase, summarize, or infer. Every heading, paragraph, button label, link, caption, badge, and tooltip must be captured verbatim.

Organize by region:
```
HEADER:     [nav items, logo text, CTA buttons]
HERO:       [headline, subheadline, CTA text]
SECTION 1:  [label, heading, body text, card titles, card descriptions]
FOOTER:     [links, copyright, etc.]
```

### 1.2 UI Structure

Identify distinct regions and their relationships:
- Container boundaries (full-width vs. constrained)
- Content hierarchy (what contains what)
- Grid/flex patterns (column counts, alignment)
- Sticky or fixed-position elements

### 1.3 Visual Measurements

Map to Tailwind utilities:

| Property | Estimation Approach |
|---|---|
| Spacing | Relative to element size → `gap-4`, `p-6`, `mb-8`, `py-12` |
| Font size | Relative hierarchy → `text-sm` through `text-6xl` |
| Font weight | Visual thickness → `font-normal`, `font-medium`, `font-semibold`, `font-bold` |
| Border radius | Shape observation → `rounded-md`, `rounded-lg`, `rounded-xl`, `rounded-full` |
| Max width | Content constraint → `max-w-5xl`, `max-w-7xl`, `max-w-screen-xl` |

### 1.4 Color Mapping to Design Tokens

Map every color in the screenshot to a semantic token from the project's design system. Think in tokens, not colors:

| What You See | Think → Token |
|---|---|
| Page background | `bg-background` |
| Card/surface background | `bg-card` |
| Subtle/muted background | `bg-muted`, `bg-secondary` |
| Primary heading text | `text-foreground` |
| Secondary/description text | `text-muted-foreground` |
| Accent-colored text | `text-accent-foreground`, `text-primary` |
| Primary action button | `bg-primary text-primary-foreground` |
| Secondary/ghost button | `bg-secondary text-secondary-foreground` |
| Borders | `border-border` |
| Hover backgrounds | `hover:bg-accent`, `hover:bg-muted` |
| Focus rings | `ring-ring` |

**CRITICAL:** If you see a color, immediately think "which token?" Never output hardcoded colors like `text-black`, `bg-white`, `text-gray-500`, `bg-[#hex]`, or any Tailwind color scale class. The only exception is `bg-[#hex]` for purely decorative elements that should NOT change with themes (rare).

### 1.5 Interactive Elements

Note every interactive pattern:
- Buttons (primary, secondary, ghost, icon-only)
- Links (inline, standalone, with icons)
- Hover states (color shifts, elevation changes, transforms)
- Active/focus states
- Dropdowns, accordions, tabs, modals
- Form elements (inputs, selects, checkboxes)
- Scroll behaviors or animations

### 1.6 Design System Alignment Check

Compare screenshot patterns against the project's DESIGN_BRIEF.md:
- Does the screenshot's spacing match the brief's spacing conventions?
- Does the typography hierarchy align?
- Are there any patterns in the screenshot that conflict with the project's Do's/Don'ts?

If conflicts exist, **prioritize the project's design system** over the screenshot. The screenshot is a reference, not a spec — the design system is the spec.

---

## Phase 2: Structure Planning

Before writing code, determine the implementation plan.

### 2.1 Semantic HTML

Map regions to semantic elements:

| Region | Element |
|---|---|
| Navigation | `<nav aria-label="...">` |
| Page section | `<section>` |
| Independent content | `<article>` |
| Footer | `<footer>` |
| Header within section | `<header>` |
| Generic grouping | `<div>` |

### 2.2 Layout Strategy

Choose the right layout model for each region:

| Pattern | Implementation |
|---|---|
| Side-by-side content | `grid grid-cols-1 md:grid-cols-2` |
| Card grid | `grid gap-6 md:grid-cols-2 lg:grid-cols-3` |
| Stacked content | `flex flex-col gap-*` |
| Centered content | `mx-auto max-w-*` or `flex items-center justify-center` |
| Asymmetric split | `grid grid-cols-1 lg:grid-cols-[2fr_1fr]` |

### 2.3 Responsive Plan

Define behavior at each breakpoint:
- **Base (mobile):** Single column, reduced spacing, smaller text
- **`md:` (768px+):** Two columns where appropriate, larger spacing
- **`lg:` (1024px+):** Full desktop layout, maximum widths, full spacing

### 2.4 Component Boundaries

Decide what is ONE component vs. what should be split:
- A self-contained card → single component
- A full page section with header + grid + CTA → single component (unless cards are reused elsewhere)
- A complex page layout → suggest splitting, ask user

---

## Phase 3: Code Generation

Generate the component in the project's framework. Follow the framework-specific patterns below.

### Vue 3 (Composition API)

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

// Images — only use files that exist in /src/graphics/
const heroImage = '/src/graphics/placeholder.jpg'
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

**Vue conventions:**
- `<script setup>` always first, then `<template>`. No `<style>` block — Tailwind handles styling.
- Use `v-for` with `:key` for lists
- Use `{{ }}` interpolation for text
- Reactive data with `ref()` / `reactive()` only when state changes are needed
- Props with `defineProps()` if the component receives data from a parent
- All text content as `const` variables in `<script setup>` — zero hardcoded strings in `<template>`

### Astro

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

const heroImage = "/src/graphics/placeholder.jpg";
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

**Astro conventions:**
- All content in frontmatter (`---` block)
- Use `{variable}` interpolation
- Arrays with `.map()` and `key` prop
- No `<style>` block — Tailwind handles styling
- Interactive behavior via `<script>` tags with vanilla JS (not TypeScript)

### Plain HTML + Tailwind

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

**HTML conventions:**
- Content inline (no data abstraction layer)
- Comment blocks for component identification
- Repeated elements written out explicitly

---

## Phase 4: Verification

Before delivering, run through this checklist. Every item must pass.

### Universal Checks

- [ ] **All visible text** from the screenshot is present and verbatim
- [ ] **All colors** use semantic design tokens — search the output for `gray`, `black`, `white`, `slate`, `zinc`, `neutral`, `stone`, `bg-[#` — there should be zero matches
- [ ] **All images** reference files that actually exist in `/src/graphics/`
- [ ] **Responsive** at mobile (base), tablet (`md:`), and desktop (`lg:`)
- [ ] **Semantic HTML** used throughout (`section`, `nav`, `article`, `footer`, etc.)
- [ ] **Spacing** matches the screenshot's proportions
- [ ] **Design system alignment** — component follows the project's DESIGN_BRIEF.md conventions
- [ ] **Hover and focus states** present on all interactive elements
- [ ] **Accessible** — ARIA labels on nav, alt text on images, logical heading hierarchy

### Framework-Specific Checks

**Vue 3:**
- [ ] All text extracted to `<script setup>` variables
- [ ] Lists use `v-for` with `:key`
- [ ] No `<style>` block (Tailwind only)
- [ ] Reactive state only where actually needed

**Astro:**
- [ ] All text extracted to frontmatter
- [ ] Arrays have `id` property for `.map()` keys
- [ ] No TypeScript in `<script>` tags

**HTML:**
- [ ] Component wrapped in a clear comment block
- [ ] Repeated elements written out (no template logic)

---

## Handling Edge Cases

**Screenshot has colors not in the design system:**
Map to the closest semantic token. If no token fits, check if the DESIGN_BRIEF.md documents an extended palette. As a last resort, define a new semantic token in the project's `global.css` `@theme` block — give it a name that fits the design system's existing naming conventions — then flag it to the user with an explanation of where it was added and why.

**Screenshot uses a different font than the design system:**
Use the project's font stack. The screenshot is a structural reference, the design system is the typographic authority.

**Screenshot shows a very complex interactive pattern (e.g., drag-and-drop, canvas):**
Implement the visual layout and static state. Add a comment block describing the interaction and suggest an appropriate library or approach. Do not attempt complex JS interactions without user confirmation.

**Screenshot is low resolution or ambiguous:**
State your assumptions explicitly before generating code. Ask the user to confirm if uncertain about specific measurements or content.

**Multiple screenshots for one component (e.g., desktop + mobile):**
Use both to inform the responsive implementation. The desktop screenshot drives `lg:` styles, mobile drives base styles.
