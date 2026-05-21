---
name: mengmeng.design
description: Personal portfolio for a graphic designer — illustration, motion, editorial, oil painting
colors:
  primary: "#[TBD]"
  secondary: "#[TBD]"
  tertiary: "#[TBD]"
  neutral-bg: "#[TBD]"
  neutral-text: "#[TBD]"
typography:
  display:
    fontFamily: "DM Mono, ui-monospace, monospace"
    fontSize: "[clamp size]"
    fontWeight: [weight]
    lineHeight: 1
  body:
    fontFamily: "DM Mono, ui-monospace, monospace"
    fontSize: "[size]"
    fontWeight: [weight]
    lineHeight: 1.5
  label:
    fontFamily: "DM Mono, ui-monospace, monospace"
    fontSize: "[size]"
    fontWeight: [weight]
    letterSpacing: "[tracking]"
rounded:
  sm: "[value]"
  md: "[value]"
spacing:
  sm: "[value]"
  md: "[value]"
  lg: "[value]"
---

# Design System: mengmeng.design

<!-- SEED: re-run /impeccable document once there's code to capture the actual tokens and components. -->

## 1. Overview

**Creative North Star: The Considered Studio**

A personal portfolio that functions as a designer's collected works — not a reel, not a resume, not a Behance grid. The site feels like stepping into a studio where the work has been placed with intention, not arranged for maximum throughput. Warm, human, and quietly confident. The dog-energy of warm-happy lives here in the approachability of the experience: nothing is cold, nothing is overwrought.

**Key Characteristics:**
- Full-palette color strategy: color is a compositional element, not decoration
- Mono-forward typography (DM Mono): one typeface across all roles creates a distinctive, precise identity
- Responsive motion: things respond to the user, they don't perform for them
- Flat by default with tonal layering; no decorative shadows
- The portfolio itself demonstrates the designer's taste — every decision is part of the work

**What this explicitly is NOT:** Behance-grid sameness, hero-reel template, mile-wide portfolio, cold-conceptual self-seriousness, portfolio-as-resume. (From PRODUCT.md Anti-references.)

## 2. Colors: The Full Palette

**Color as composition.** This is not a restrained "accent on neutrals" system. Color has named roles and is used deliberately across the surface — not decoratively, but structurally.

**The Full Palette Rule.** Three to four named color roles, each with a specific purpose. No color is accidental. No role is filler.

### Primary
- **[TBD: primary role color]** (`#XXXXXX` / oklch(...)): [Primary brand accent. Used for key interactive elements, focal points, and moments of intentional emphasis.]

### Secondary
- **[TBD: secondary role color]** (`#XXXXXX` / oklch(...)): [Supporting accent. Used to create rhythm and hierarchy within components.]

### Tertiary
- **[TBD: tertiary role color]** (`#XXXXXX` / oklch(...)): [Tertiary accent. Used sparingly for variety and compositional balance.]

### Neutral
- **[TBD: warm neutral]** (`#XXXXXX` / oklch(...)): [Warm-tinted neutral for backgrounds and text. Tint every neutral toward the brand hue — chroma 0.005–0.01 is enough. Never use #000 or #fff.]
- **[TBD: neutral text]** (`#XXXXXX` / oklch(...)): [Body text, secondary text, borders.]

## 3. Typography

**Font:** DM Mono (with `ui-monospace, monospace` as fallbacks)

**Character:** One typeface doing multiple jobs — from hero headlines to body text to metadata labels. The mono-forward identity is itself a design statement: this is a designer who treats all type as precise and intentional, not just labels as an afterthought. DM Mono carries enough optical weight and personality to work at display sizes while remaining legible as body text.

### Hierarchy
- **Display** ([weight], [size/clamp], [line-height]): Hero headlines, project titles. The largest typographic moment.
- **Headline** ([weight], [size], [line-height]): Section headers, major labels.
- **Title** ([weight], [size], [line-height]): Sub-labels, metadata.
- **Body** ([weight], [size], [line-height]): Running text, project descriptions. Max 65–75ch line length.
- **Label** ([weight], [size], [letter-spacing], [case]): Tags, dates, categories. Mono font here.

**The Display Rule.** Display type is used only where it earns its place — headlines, hero moments, project titles. Never decorative body text or UI labels.

**The Mono Metadata Rule.** Mono appears on labels, metadata, and technical details. It never replaces display or body; its precision is the point.

## 4. Elevation

**Flat by default with tonal layering.** This system does not reach for shadows to solve hierarchy problems. Depth is conveyed through tonal contrast (light vs. dark variants within a hue family) and spatial spacing.

No decorative shadows. Shadows appear only as a functional response to state — a hover, an elevation request, a focus indicator.

**The No-Decorative-Shadow Rule.** Shadows are functional, not decorative. If a shadow isn't communicating something about state or hierarchy, it doesn't exist.

## 5. Components

*(Seed stage — no components exist yet. Components will be documented on the next /impeccable document run once code exists.)*

## 6. Do's and Don'ts

### Do:
- **Do** use color as a compositional element with named roles — primary, secondary, tertiary, neutral.
- **Do** let the work lead. The site exists to present work, not to perform the designer's personality.
- **Do** use display type for headlines and project titles only — never as decoration.
- **Do** use mono for metadata, labels, and technical details — its precision is the point.
- **Do** keep motion responsive: feedback and transitions that respond to user intent, not choreography.
- **Do** convey depth through tonal contrast and spacing before reaching for shadows.

### Don't:
- **Don't** use the Behance-grid template — uniform cards, hover-reveal interactions, three-section hero-about-skills structure. (PRODUCT.md Anti-reference.)
- **Don't** use hero-reel template — full-screen video loops as a substitute for curation. (PRODUCT.md Anti-reference.)
- **Don't** present work as a mile-wide portfolio — "I do branding, UI, motion, illustration, art direction, 3D..." (PRODUCT.md Anti-reference.)
- **Don't** use cold-conceptual presentation — work so self-serious it serves awards rather than clients. (PRODUCT.md Anti-reference.)
- **Don't** lead with "about me" before showing work. (PRODUCT.md Anti-reference.)
- **Don't** use #000 or #fff as a neutral. Tint every neutral toward the brand hue.
- **Don't** use shadows decoratively. Shadows are functional only.
- **Don't** animate CSS layout properties.
- **Don't** use bounce or elastic easing — ease-out-quart or ease-out-expo only.