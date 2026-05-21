---
name: mengmeng.design
description: Personal portfolio for a graphic designer — illustration, motion, editorial, oil painting
register: brand
colors:
  primary:
    value: "oklch(65% 0.14 45)"
    usage: "Key interactive elements, focal points, category labels, hover states."
  primary-hover:
    value: "oklch(58% 0.16 45)"
    usage: "Interactive element hover/active states."
  secondary:
    value: "oklch(55% 0.10 200)"
    usage: "Supporting accent. Reserved for future use."
  tertiary:
    value: "oklch(65% 0.10 10)"
    usage: "Tertiary accent. Reserved for future compositional balance."
  neutral-bg:
    value: "oklch(97% 0.006 50)"
    usage: "Page background. Warm-tinted, never pure white."
  neutral-surface:
    value: "oklch(94% 0.008 50)"
    usage: "Card backgrounds, elevated surfaces."
  neutral-text:
    value: "oklch(25% 0.010 50)"
    usage: "Body text, primary labels. Warm-tinted, never pure black."
  neutral-muted:
    value: "oklch(55% 0.008 50)"
    usage: "Secondary text, descriptions, metadata."
  neutral-border:
    value: "oklch(85% 0.008 50)"
    usage: "Borders, dividers, separators."
typography:
  fontFamily: "DM Mono, ui-monospace, monospace"
  display:
    weight: 200
    size: "clamp(3rem, 8vw, 5.5rem)"
    lineHeight: 1.1
    letterSpacing: "-0.04em"
  headline:
    weight: 300
    size: "clamp(1.5rem, 3vw, 2rem)"
    lineHeight: 1.1
    letterSpacing: "-0.02em"
  title:
    weight: 400
    size: "1rem"
    lineHeight: 1.3
  body:
    weight: 400
    size: "1rem"
    lineHeight: 1.6
  small:
    weight: 400
    size: "0.8125rem"
    lineHeight: 1.6
  label:
    weight: 500
    size: "0.6875rem"
    letterSpacing: "0.15em"
    textTransform: "uppercase"
spacing:
  "2xs": "0.25rem"
  "xs": "0.5rem"
  "sm": "0.75rem"
  "md": "1rem"
  "lg": "1.5rem"
  "xl": "2rem"
  "2xl": "3rem"
  "3xl": "4rem"
  "4xl": "6rem"
  "5xl": "8rem"
radius:
  sm: "3px"
  md: "6px"
  lg: "12px"
motion:
  ease-out-quart: "cubic-bezier(0.25, 1, 0.5, 1)"
  ease-out-expo: "cubic-bezier(0.16, 1, 0.3, 1)"
  duration-fast: "150ms"
  duration-base: "250ms"
  duration-slow: "400ms"
layout:
  max-width: "1200px"
  content-width: "72ch"
  gutter: "clamp(1rem, 4vw, 2rem)"
---

# Design System: mengmeng.design

## 1. Overview

**Creative North Star: The Considered Studio**

A personal portfolio that functions as a designer's collected works — not a reel, not a resume, not a Behance grid. The site feels like stepping into a studio where the work has been placed with intention, not arranged for maximum throughput. Warm, human, and quietly confident.

**Key Characteristics:**
- Full-palette color strategy: color is a compositional element, not decoration
- Mono-forward typography (DM Mono): one typeface across all roles creates a distinctive, precise identity
- Responsive motion: things respond to the user, they don't perform for them
- Flat by default with tonal layering; no decorative shadows
- The portfolio itself demonstrates the designer's taste — every decision is part of the work

## 2. Colors: The Full Palette

Color roles are established and used deliberately. No accidental color. No role is filler.

**Primary — warm coral/amber** (`oklch(65% 0.14 45)`)
Used for: category labels on work cards, nav wordmark hover, selection highlight, focus rings.

**Secondary — warm teal** (`oklch(55% 0.10 200)`)
Reserved. Intended for future compositional rhythm.

**Tertiary — dusty rose** (`oklch(65% 0.10 10)`)
Reserved. Intended for future variety and compositional balance.

**Neutral — warm-tinted, never pure**
- `oklch(97% 0.006 50)` — page background
- `oklch(94% 0.008 50)` — card/image backgrounds
- `oklch(25% 0.010 50)` — body text
- `oklch(55% 0.008 50)` — secondary text, descriptions
- `oklch(85% 0.008 50)` — borders, dividers

**The Tint Rule.** Every neutral is tinted toward the brand hue. Chroma 0.006–0.010 is sufficient. `#000` and `#fff` are never used.

## 3. Typography

**Font:** DM Mono (with `ui-monospace, monospace` as fallbacks)

One typeface across all roles: display, body, label, metadata. The mono-forward identity is itself a design statement — all type is precise and intentional.

### Hierarchy

| Role | Weight | Size | Line Height | Letter Spacing | Notes |
|------|--------|------|-------------|----------------|-------|
| Display | 200 | clamp(3rem, 8vw, 5.5rem) | 1.1 | -0.04em | Hero headlines, stacked three-line layout |
| Headline | 300 | clamp(1.5rem, 3vw, 2rem) | 1.1 | -0.02em | Page titles, section headers |
| Body | 400 | 1rem | 1.6 | — | Running text, project descriptions |
| Small | 400 | 0.8125rem | 1.6 | — | Secondary descriptions |
| Label | 500 | 0.6875rem | — | 0.15em | All-caps, category tags, dates, years |

**The Display Rule.** Display type earns its place at hero moments and project titles. Never decorative.

**The Mono Metadata Rule.** Mono appears on labels, metadata, and technical details. Its precision is the point.

## 4. Spacing

Fluid scale from `0.25rem` to `8rem`. Spacing varies for rhythm — same padding everywhere is monotony.

## 5. Elevation

**Flat by default with tonal layering.** No decorative shadows. Borders and background tints create depth.

The gradient overlay on images (transparent to `oklch(0% 0 0 / 0.06)`) creates image-to-content transition without shadow.

## 6. Motion

**Responsive, not choreographed.** Things respond to the user — they don't perform.

- Hover states: `150ms` ease-out-quart
- Image zoom: `400ms` ease-out-quart at `scale(1.03)`
- `prefers-reduced-motion` respected globally: animation-duration `0.01ms`, transition-duration `150ms`

**No bounce, no elastic.** Ease-out-quart and ease-out-expo only.

## 7. Components

### Header (Base.astro)
Sticky, `z-index: 100`. Contains nav wordmark and links. Background uses `--color-neutral-bg` with `1px` border-bottom. Height: `4rem`.

### Footer (Base.astro)
Flex row with copyright and social links. Top border `1px` using `--color-neutral-border`. Uses `--text-small`.

### Hero (index.astro)
Stacked layout: eyebrow (label, primary color) → heading (display, 3-line stacked via `<br>`) → sub (body-weight, small size). Eyebrow has `0.2em` letter-spacing. Heading has `-0.04em` tracking. Sub max-width `36ch`.

### Work List — Home Page (index.astro)
2-column grid of featured projects. Each item: image (4/3 aspect, overlay gradient) + meta (category label → name → description → year). Hover: `scale(1.03)`, `400ms` ease-out-quart. `loading={index < 2 ? 'eager' : 'lazy'}`.

### Work Grid — /work Page (work/index.astro)
3-column grid of all projects. Server-rendered. Image treatment same as home page. Meta includes category label, title, description paragraph, year. Grid gap: `4rem / 3rem`.

### About Page (about.astro)
Two-column: image left, text right. Uses `<figure>` and `<figcaption>` for image attribution. Body copy stripped of first-person voice.

## 8. Technical

**Framework:** Astro 6 (static output, no adapter)
**Fonts:** Google Fonts (DM Mono, preconnected)
**Colors:** OKLCH throughout
**Build output:** `dist/` — static HTML/CSS, no JS required for content
**Deploy:** GitHub Pages via `.github/workflows/deploy.yml` (Node 22)
**No framework JavaScript.** Component interactivity via minimal inline `<script>` blocks where needed.

## 9. Do's and Don'ts

### Do:
- Use color as a compositional element with named roles — primary, secondary, tertiary, neutral
- Let the work lead. The site exists to present work, not to perform the designer's personality
- Use display type for headlines and project titles only — never as decoration
- Use mono for metadata, labels, and technical details
- Keep motion responsive: feedback and transitions that respond to user intent, not choreography
- Convey depth through tonal contrast and spacing before reaching for shadows

### Don't:
- Use the Behance-grid template (uniform card layouts, hover-reveal)
- Use hero-reel template (full-screen video loops)
- Present work as a mile-wide portfolio
- Use cold-conceptual presentation (self-serious for awards not clients)
- Lead with "about me" before showing work
- Use `#000` or `#fff` as a neutral
- Use shadows decoratively — only functional
- Animate CSS layout properties
- Use bounce or elastic easing
- Use em dashes — only colons, commas, periods, parentheses