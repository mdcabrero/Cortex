# Verification Checklist

Run through every item before delivering. All must pass.

---

## Universal Checks

- [ ] **All visible text** from the screenshot is present and verbatim
- [ ] **All colors** use semantic design tokens — search the output for `gray`, `black`, `white`, `slate`, `zinc`, `neutral`, `stone`, `bg-[#` — there should be zero matches
- [ ] **All images** reference files that actually exist in the project's image directory
- [ ] **Responsive** at mobile (base), tablet (`md:`), and desktop (`lg:`)
- [ ] **Semantic HTML** used throughout (`section`, `nav`, `article`, `footer`, etc.)
- [ ] **Spacing** matches the screenshot's proportions
- [ ] **Design system alignment** — component follows the project's DESIGN_BRIEF.md conventions
- [ ] **Hover and focus states** present on all interactive elements
- [ ] **Accessible** — ARIA labels on nav, alt text on images, logical heading hierarchy

---

## Framework-Specific Checks

### Vue 3
- [ ] All text extracted to `<script setup>` variables
- [ ] Lists use `v-for` with `:key`
- [ ] No `<style>` block (Tailwind only)
- [ ] Reactive state only where actually needed

### Astro
- [ ] All text extracted to frontmatter
- [ ] Arrays have `id` property for `.map()` keys
- [ ] No TypeScript in `<script>` tags

### HTML
- [ ] Component wrapped in a clear comment block
- [ ] Repeated elements written out (no template logic)
