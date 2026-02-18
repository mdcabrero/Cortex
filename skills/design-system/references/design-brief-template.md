# Design Brief: [PROJECT_NAME]

## Project Overview

[1–2 paragraph summary of the project and what this design system serves. State the primary theme direction (dark-first or light-first) and the overall goal of the visual identity.]

---

## Core Aesthetic Direction

### Visual Identity: **[Aesthetic Name]**

[2–3 sentences capturing the essence of the visual identity in evocative, precise language. This should read like a creative brief — not a technical spec.]

**Design Philosophy:**

[An expanded articulation of the guiding principles behind every visual decision in this system. This section should be the most thoughtful and expressive in the entire document. Address:]

- What emotional response should the interface evoke?
- What tension or balance does the design deliberately strike? (e.g., "minimal yet warm", "bold yet restrained", "dense yet breathable")
- What design conventions does it follow, and which does it intentionally break?
- How does the visual language reinforce the product's purpose or brand?
- What is the relationship between content and ornamentation?

[Write this as connected prose, not a checklist. The goal is that any designer reading this section could make confident visual decisions for new screens without seeing the original references.]

**Key Characteristics:**

- [Characteristic 1 — e.g., "Dramatic dark foundation with rich depth"]
- [Characteristic 2 — e.g., "Bold serif headlines that command attention"]
- [Characteristic 3 — e.g., "Strategic accent colors that punctuate without overwhelming"]
- [Characteristic 4 — e.g., "Generous negative space creating breathing room"]
- [Characteristic 5 — e.g., "Warm undertones preventing sterile coldness"]
- [Characteristic 6 — e.g., "Card-based architecture with subtle elevation"]

**Influences & References:**

[Briefly note the visual influences or reference points that inform this aesthetic. These could be design movements, specific websites, artistic traditions, or product categories. This helps future designers understand the lineage of the design decisions.]

---

## Color System

### Primary Palette

```css
/* Foundation */
--color-[name]: [HEX];         /* [Role description] */
--color-[name]: [HEX];         /* [Role description] */

/* Accents */
--color-[name]: [HEX];         /* [Role description] */
--color-[name]: [HEX];         /* [Role description] */

/* Typography */
--color-[name]: [HEX];         /* [Role description] */
--color-[name]: [HEX];         /* [Role description] */
```

### Usage Guidelines

**[Color Name] ([HEX])**
- [Usage context 1]
- [Usage context 2]
- [Usage context 3]
- [Design guidance — when/how to use, when NOT to use]

[Repeat for each color in the palette]

### Counterpart Variant

[Describe the approach taken for the alternative theme. Explain which colors shift, how the accent colors adapt, and what the overall feel of the counterpart is. Note any specific contrast considerations.]

---

## Typography

### Font Stack

| Role | Family | Fallback | Usage |
|------|--------|----------|-------|
| Display / Headlines | [Font Name] | [serif/sans-serif] | [Where used] |
| Body / Text | [Font Name] | [serif/sans-serif] | [Where used] |
| Mono / Code | [Font Name] | [monospace] | [Where used] |

### Type Scale & Hierarchy

[Describe the typographic hierarchy observed in the reference screenshots:]

- **Hero headlines**: [size range, weight, font family, any special treatments like letter-spacing]
- **Section headlines**: [size range, weight, font family]
- **Card/feature titles**: [size range, weight, font family]
- **Body text**: [size, weight, line-height guidance]
- **Secondary/muted text**: [size, weight, color token]
- **Labels/badges**: [size, weight, letter-spacing, text-transform]

### Typography Principles

[2–3 sentences on the overall typographic philosophy — e.g., "Headlines use a high-contrast serif to create visual drama against the dark background, while body text relies on a clean sans-serif for sustained readability. The scale jumps are intentionally dramatic to create clear hierarchy without relying on color alone."]

---

## Layout Principles

### Spatial Composition

**Content Width:** [max-width value, centering strategy]

**Spacing Scale:**
- Section-to-section: [value range, e.g., 80px–120px]
- Card internal padding: [value range, e.g., 24px–48px]
- Element-to-element: [value range, e.g., 16px–24px]
- Card grid gaps: [value range, e.g., 24px–32px]

**Grid System:**
- [Column count and flexibility]
- [Asymmetric vs. symmetric tendencies]
- [Breakpoint behavior notes]

**Spatial Philosophy:**
[1–2 sentences — e.g., "Embrace negative space generously. Don't crowd the interface — let it breathe. Whitespace is a design element, not wasted space."]

### Elevation & Depth

**Border Treatment:**
- [Border color approach — e.g., translucent white at low opacity, never solid]
- [Border width standard]
- [Border radius range]

**Shadow Strategy:**
- [Overall approach — flat, subtle, dramatic]
- [Hover state shadow behavior]
- [Interaction between shadows and background color]

---

## Component Patterns

[Describe the recurring UI patterns observed in the screenshots. Do NOT provide component code — describe the visual patterns so designers can implement them consistently.]

### Cards

- [Background treatment]
- [Border treatment]
- [Padding and spacing]
- [Hover behavior]
- [Content structure within cards]

### Buttons

**Primary:** [Visual description — color, shape, padding, hover state]
**Secondary:** [Visual description — color, shape, padding, hover state]
**Ghost/Text:** [If observed — visual description]

### Badges & Labels

- [Shape, size, color treatment]
- [Text style within badges]
- [Common variants observed]

### Navigation

- [Style of navigation observed]
- [Active/hover states]
- [Sticky/fixed behavior]

### Images & Media

- [Image treatment — overlays, borders, radius]
- [Aspect ratio tendencies]
- [Caption or label placement]

---

## Motion & Interaction

### Animation Strategy

**Overall Approach:** [e.g., "Subtle and purposeful — avoid excessive motion"]

**Hover States:**
- [Card hover behavior]
- [Button hover behavior]
- [Link hover behavior]
- [Transition duration and easing]

**Page Load / Entrance Animations:**
- [Reveal strategy — stagger, fade, slide]
- [Duration and delay values]
- [Which elements animate on load vs. which are static]

**Scroll Behavior:**
- [Smooth scroll, parallax, sticky elements]
- [Intersection observer patterns if applicable]

### Easing Reference

- Default transitions: [easing function, e.g., `cubic-bezier(0.4, 0, 0.2, 1)`]
- Duration range: [e.g., 150ms–600ms depending on element size]

---

## Visual Details & Atmosphere

[Document any special visual treatments that give the design its unique character.]

### Textures & Effects

[Only include subsections that are relevant to the aesthetic. Delete unused ones.]

**Gradients:**
- [Gradient usage, direction, color stops]
- [Where applied — backgrounds, overlays, decorative elements]

**Grain / Noise:**
- [If used — opacity, pattern type, where applied]

**Glassmorphism / Blur:**
- [If used — blur values, background opacity, border treatment]

**Glow / Light Effects:**
- [If used — color, spread, where applied]

### Selection & Focus

- Text selection: [color treatment]
- Focus rings: [color, offset, style]
- Scrollbar: [custom styled or default]

---

## Do's and Don'ts

### DO:
- ✓ [Specific positive guidance tied to THIS aesthetic]
- ✓ [Specific positive guidance tied to THIS aesthetic]
- ✓ [Specific positive guidance tied to THIS aesthetic]
- ✓ [Specific positive guidance tied to THIS aesthetic]
- ✓ [Specific positive guidance tied to THIS aesthetic]

### DON'T:
- ✗ [Specific anti-pattern for THIS aesthetic]
- ✗ [Specific anti-pattern for THIS aesthetic]
- ✗ [Specific anti-pattern for THIS aesthetic]
- ✗ [Specific anti-pattern for THIS aesthetic]
- ✗ [Specific anti-pattern for THIS aesthetic]

[These should be highly specific to the design direction, NOT generic design advice. Every item should help a designer make a judgment call specific to this system.]

---

## Accessibility Requirements

### Contrast Ratios

| Combination | Ratio | Level |
|---|---|---|
| [Text color] on [Background color] | [X:1] | [AA/AAA] |
| [Text color] on [Card color] | [X:1] | [AA/AAA] |
| [Muted text] on [Background color] | [X:1] | [AA/AAA] |
| [Accent color] on [Background color] | [X:1] | [AA/AAA] |

### Focus States

- [Focus indicator color and style]
- [Focus offset]
- [Keyboard navigation approach]

### Structural Accessibility

- Semantic HTML expectations (header, nav, main, section, footer)
- Heading hierarchy (h1 → h6)
- ARIA label requirements for interactive elements
- Skip-to-content link