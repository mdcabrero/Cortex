---
name: design-system
description: Generate complete Tailwind CSS v4 design systems from color palettes and visual references. Use this skill whenever the user wants to create a design system, theme, or styling foundation for a website or application. Triggers include requests for a design system, theme, global.css, design tokens, color system, or when the user provides a color palette and/or UI screenshots and wants a cohesive styling foundation built from them. Also use when the user says things like create a design system from these screenshots, build me a theme based on this site, or generate a Tailwind config from these colors. Do NOT use for one-off component styling, individual page builds, or tasks better suited to the frontend-design skill.
---

# Design System Generator

Generate production-ready Tailwind CSS v4 design systems from a base color palette and visual reference screenshots. Outputs a complete `global.css` theme file using semantic tokens in shadcn/oklch structure, and a comprehensive `DESIGN_BRIEF.md` documenting the full visual identity.

---

## Inputs

The user provides:

1. **Color palette** (required) — A small set of ~4–8 backbone colors with descriptive labels. Example:
   ```
   MAIN DARK: #0F0E0D
   DARK GRANITE (cards/modals): #252423
   BOLD ORANGE (accent #1): #F76B15
   SOFT PASTEL (accent #2): #FFC1F2
   PURE WHITE (main text): #FFFFFF
   SLATE GRAY (secondary text): #86857D
   ```

2. **Reference screenshots** (required) — 4–5 screenshots from different pages/sections of an existing application, landing page, or website that represent the target aesthetic.

3. **Font preferences** (optional) — If the user provides specific font families, use them. If not, infer appropriate fonts from the screenshots and overall aesthetic direction.

---

## Workflow

This skill follows a strict **analyze → interpret → approve → plan → generate** workflow. Do not skip steps or jump ahead to file generation.

### Phase 1: Screenshot Analysis

Examine every screenshot carefully. Extract observations at two priority levels:

**Priority 1 — Aesthetic Mood (most important):**
- Overall visual personality and feeling (e.g., "dark luxe minimal", "warm brutalist", "soft editorial", "neon cyberpunk")
- Emotional tone the design evokes (confidence, playfulness, warmth, coldness, refinement, rawness)
- Design philosophy: what principles seem to guide every decision?
- Key tension or balance the design strikes (e.g., "minimal yet warm", "bold yet restrained", "dense yet readable")

**Priority 2 — Element-Level Details:**
- Visual density and spacing patterns (generous whitespace vs. tight layouts)
- Typography hierarchy: how many levels, relative sizes, weight distribution, serif vs. sans-serif usage
- Border radius tendencies (sharp, slightly rounded, heavily rounded, pill-shaped)
- Shadow and elevation strategy (flat, subtle depth, dramatic shadows, layered)
- Border treatment (none, subtle/translucent, prominent, decorative)
- Color distribution: which colors dominate, which are used sparingly as accents
- Special visual treatments (gradients, grain/noise textures, glassmorphism, overlays, blend modes)

### Phase 2: Present Interpretation

Present a thorough written interpretation of the aesthetic to the user. This is a conversation — the user must approve or provide feedback before proceeding. Structure the interpretation as:

1. **Aesthetic Direction** — A descriptive name and 2–3 sentence summary of the visual identity
2. **Design Philosophy** — The guiding principles behind every visual decision
3. **Key Characteristics** — Bullet list of the defining traits observed
4. **Color Role Mapping** — How the user's provided colors map to semantic roles (background, foreground, card, muted, accent, primary, destructive, etc.)
5. **Typography Plan** — Proposed font pairing and hierarchy (use provided fonts or suggest based on aesthetic)
6. **Special Treatments** — Any gradients, textures, or atmospheric effects worth encoding as utility classes

Wait for user approval or feedback. Iterate if needed.

### Phase 3: Plan

Once the user approves the interpretation, present a brief plan covering:

- Confirmation of the primary theme direction (dark-first or light-first)
- The counterpart variant approach (light or dark accessible alternative)
- Which aesthetic utility classes will be generated (if any)
- Font imports needed
- Any custom keyframe animations that suit the aesthetic

Wait for user confirmation before generating.

### Phase 4: Generate

Produce two files:

1. **`global.css`** — Complete Tailwind v4 design system
2. **`DESIGN_BRIEF.md`** — Comprehensive visual identity document

Read the reference templates before generating:
```
Read references/token-template.css    # Semantic token structure to follow
Read references/design-brief-template.md     # Design brief structure to follow
```

---

## Output Specifications

### global.css

The CSS file follows the **shadcn/oklch semantic token** pattern. Key rules:

- **All colors as oklch values** in CSS custom properties. Convert the user's hex colors to oklch.
- **Semantic token naming** — Use the standard set: `--background`, `--foreground`, `--card`, `--card-foreground`, `--popover`, `--popover-foreground`, `--primary`, `--primary-foreground`, `--secondary`, `--secondary-foreground`, `--muted`, `--muted-foreground`, `--accent`, `--accent-foreground`, `--destructive`, `--border`, `--input`, `--ring`, `--chart-1` through `--chart-5`, and the full `--sidebar-*` set.
- **`:root` block** for the primary theme, **`.dark` or `.light` variant** for the counterpart.
- **`@theme inline` block** mapping CSS variables to Tailwind's `--color-*`, `--radius-*`, `--shadow-*`, `--font-*` namespace.
- **Font imports** at the top (Google Fonts or similar CDN).
- **Shadows** calibrated to the aesthetic (subtle for minimal, dramatic for bold).
- **Border radius scale** matching the observed style.
- **Keyframe animations** that suit the aesthetic (fade-in, slide-up, accordion, progress, etc.).
- **Aesthetic utility classes** ONLY when the style demands them — gradients, grain textures, glassmorphism, glow effects, etc. These are atmospheric helpers, not component classes.
- **No component classes** — no `.btn-primary`, `.card`, `.modal`, etc. Those are built individually.

**Color Expansion Logic:**

The user provides ~6 backbone colors. Expand them into the full semantic set:

| User Input | Typical Semantic Mapping |
|---|---|
| Main background color | `--background` |
| Card/surface color | `--card`, `--popover`, `--secondary`, `--muted` |
| Primary accent | `--primary`, `--ring`, `--chart-1`, `--sidebar-primary` |
| Secondary accent | `--accent`, `--sidebar-accent` |
| Main text color | `--foreground`, `--card-foreground`, `--popover-foreground` |
| Secondary text color | `--muted-foreground` |

Derive additional tokens by adjusting lightness/chroma of the backbone colors. For chart colors, create a harmonic progression from the primary accent. For `--destructive`, choose a red that fits the palette's warmth/coolness. For `--border` and `--input`, derive from the card color with slight lightness adjustment.

**Counterpart Variant:**

Generate an accessible alternative, not a literal inversion. The counterpart should:
- Maintain the brand personality and feel
- Keep accent colors recognizable (adjust lightness/chroma for contrast, not hue)
- Ensure all text passes WCAG AA contrast minimums
- Feel like a deliberate design choice, not an automated flip

### DESIGN_BRIEF.md

This document references **actual color names and hex values**, not semantic tokens. It is the human-readable identity guide. Follow the template in `references/design-brief-template.md`. Key principles:

- The **Core Aesthetic Direction** section should be the most expansive — it articulates the design philosophy in depth
- The **Color System** section shows the real colors with their names, hex values, and usage guidelines
- Layout, motion, and visual detail sections describe patterns observed from the screenshots
- Do's and Don'ts are specific to the aesthetic, not generic design advice
- Accessibility section documents actual contrast ratios between key color pairs

---

## Important Distinctions

- **`global.css` uses semantic tokens** (`--primary`, `--background`, etc.) in oklch — framework-agnostic, swappable
- **`DESIGN_BRIEF.md` uses real color names and hex values** (`Bold Orange #F76B15`, `Main Dark #0F0E0D`) — human-readable identity reference
- These serve different purposes: the CSS is for machines/frameworks, the brief is for humans/designers
- Keep this separation clean. Do not leak semantic token names into the brief or hex values into the CSS.

---

## Edge Cases

- **Light-first designs**: `:root` holds the light theme, `.dark` holds the counterpart. Detect from screenshots.
- **Monochromatic palettes**: Expand using lightness variations. Generate chart colors by introducing subtle chroma shifts.
- **Very colorful palettes (8+ colors)**: Map the most structurally important colors to semantic roles. Document extras in the brief as "extended palette" with suggested use cases.
- **No clear accent color**: Derive one from the dominant hue with increased chroma.
- **Glassmorphism / transparency-heavy designs**: Create `backdrop-filter` utility classes. Note in the brief that these require appropriate background context.