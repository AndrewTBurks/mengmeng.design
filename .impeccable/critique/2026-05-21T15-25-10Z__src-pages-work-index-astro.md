---
target: /work page — src/pages/work/index.astro
total_score: 20
p0_count: 1
p1_count: 2
timestamp: 2026-05-21T15-25-10Z
slug: src-pages-work-index-astro
---
# Design Critique — /work page

## Design Health Score

| # | Heuristic | Score | Key Issue |
|---|-----------|-------|-----------|
| 1 | Visibility of System Status | 1/4 | No scroll progress, no "N of 6" context. Focal row system provides no feedback about why rows are faded. |
| 2 | Match System / Real World | 2/4 | Timeline with year markers maps to chronological portfolio. But focal row is an invented UX puzzle, not a real-world affordance. |
| 3 | User Control and Freedom | 2/4 | Focal row fade strips agency — cannot view full portfolio at full opacity without scrolling to an arbitrary position. |
| 4 | Consistency and Standards | 3/4 | DM Mono everywhere, coral primary, warm-tinted oklch system all coherent. Reduced motion respected. |
| 5 | Error Prevention | 3/4 | Focus states on image links. aria-label on links. "Coming soon" aria-hidden. No destructive actions present. |
| 6 | Recognition Rather Than Recall | 3/4 | Simple, consistent UI. Nav always visible. Layout learnable. |
| 7 | Flexibility and Efficiency of Use | 1/4 | No keyboard shortcuts. No sort/filter. Timeline constrains more than it enables. |
| 8 | Aesthetic and Minimalist Design | 2/4 | Clean but clinical. Timeline structure is neutral — not particularly creative or warm despite brand promise. |
| 9 | Error Recovery | 2/4 | No visible error states. Broken project links produce empty states with no recovery path. |
| 10 | Help and Documentation | 1/4 | No help system. No FAQ. No contact prompt on the page itself. |
| **Total** | | **20/40** | **Poor — significant improvements needed** |

---

## Anti-Patterns Verdict

**LLM Assessment: Not AI slop.** The design is hand-authored with intentional craft. No gradient text, no side-stripe borders, no hero-metric template, no identical card grids, no glassmorphism. The CSS uses a coherent OKLCH token system with purposeful easing curves.

**However: The focal row fade mechanic IS an anti-pattern for a portfolio.** It is the kind of interaction a developer would build to show technical capability rather than one that serves the viewer's discovery goal. It forces a focal point at index 2 (Motion Identity, 2023) not because it is the best work but because of array position.

**Deterministic scan**: Bundled antipattern detector unavailable (detector engine missing from skill installation). No automated rule violations found in static scan.

**Visual verification**: Timeline renders with centered vertical rule, alternating [IMAGE]||[META] / [META]||[IMAGE] layout, year bubbles (coral circles) centered on the rule. All 6 projects confirmed in DOM.

---

## Overall Impression

The /work page has a clean visual structure and a coherent token system. The coral year bubble is a strong signature element. The problem is the focal row fade — it was an interesting interactive idea, but it actively interferes with the primary job of a portfolio page: show the work clearly.

The design is technically competent but emotionally flat. For a portfolio that promises "Creative, Unique, Warm-happy," the timeline reads as a system exercise, not a curated experience. The single biggest opportunity is replacing the focal row mechanic with something that lets the work breathe.

---

## What's Working

1. **Coral year bubble as rhythmic anchor.** The `box-shadow: 0 0 0 4px var(--color-neutral-bg)` cutout effect against the vertical rule is a signature visual move. Strong, repeatable, distinctive.

2. **OKLCH token system with warm-tinted neutrals.** Never pure black or white. Spacing scale, easing curves (`--ease-out-quart`), and duration scale are internally consistent. Reduced-motion support at both HTML and component level is well-implemented.

3. **DM Mono as a deliberate typographic voice.** Mono throughout is a bold choice that actually works here — it creates a studio-notebook precision that complements illustration, motion, and editorial work. Label treatment (0.15em letter-spacing, uppercase) creates hierarchy without font switching.

---

## Priority Issues

### P0 — Focal row mechanic breaks portfolio viewing
**What**: All rows start at opacity 0.4. Only the middle row (index 2) and its siblings when scrolled into view reach full opacity. The focal point is determined by array position, not by quality or intent.
**Why it matters**: Portfolio visitors need to see work clearly. Faded rows actively inhibit evaluation. An employer who scrolls and sees dim/bright rows will think either "this is a bug" or "this designer prioritizes cleverness over clarity."
**Fix**: Remove the fade mechanic entirely. Replace with a clean vertical list where each project is clearly presented. If focal emphasis is needed, use size (hero row for best work) or a single "featured" row — not a dynamic opacity system.
**Suggested command**: `polish` or `distill`

### P1 — Redundant copy in page header
**What**: "Illustration, motion, editorial, oil painting." (subtitle) and "Spanning illustration, motion design, editorial layout, and oil painting." (work-intro) say the same thing in back-to-back elements. Second sentence "Work made with care for the details that make it worth noticing." is generic.
**Why it matters**: Redundant copy signals the designer didn't care enough to edit. Clients and employers notice these things.
**Fix**: Make the work-intro speak to the designer, not the disciplines. Or remove the work-intro entirely if the subtitle is sufficient.
**Suggested command**: `clarify`

### P1 — Dead CSS selectors (`.row-left` / `.row-right`)
**What**: Lines 360-376 define `.row-left` and `.row-right` rules in CSS but these classes are never applied to any HTML element. The grid layout uses `.row-image-left` / `.row-image-right` on `<article>` instead.
**Why it matters**: Dead code indicates drift. It will confuse future maintainers and adds no value.
**Fix**: Audit and remove `.row-left` / `.row-right` block. Also remove the unused `.row-content` wrapper div rule (padding-top: 6px).
**Suggested command**: `polish`

### P2 — No scroll progress context
**What**: With 6 projects in a vertical timeline, the viewer has no sense of where they are or how much is left. No "01 / 06" counter. No progress bar.
**Why it matters**: Portfolio visitors want to know if they're seeing the best work or if they should keep scrolling. Context reduces anxiety and encourages completion.
**Fix**: Add "01 / 06" project counter in the meta section, or a thin scroll-linked progress bar at the top of the page.
**Suggested command**: `layout` or `polish`

### P2 — ":active" state identical to default on image links
**What**: The `:active` state on `.row-image-link` (lines 398-401) resets blur to 12px and scale to 1.04 — identical to the default resting state. Clicking produces no visible feedback.
**Why it matters**: Active feedback is a core interaction signal. The absence breaks the feedback loop for users who press (not just hover) interactive elements.
**Fix**: Either remove the `:active` block if no distinct press state is needed, or make it visually distinct (deeper shadow, color shift, scale reduction).
**Suggested command**: `polish`

### P3 — Meta column max-width too narrow at 28ch for some content
**What**: "Experimental typographic posters combining letterpress and digital." (62 chars) is tight at 28ch. On desktop viewports between 1024-1200px, the row may be narrower than expected.
**Why it matters**: Minor layout compression won't break anything, but long descriptions will wrap awkwardly in the meta column.
**Fix**: Test at 1024px viewport. Consider `max-width: 32ch` or letting meta flex naturally in the grid cell.
**Suggested command**: `layout`

---

## Persona Red Flags

**Samira (Potential Employer)**: Scrolls to portfolio, sees rows at 0.4 opacity. Thinks "is this broken?" or "why can't I see the work clearly?" Assumes the designer cares more about clever interactions than clear communication. Won't spend time decoding the focal row mechanic — she'll assume the worst and leave. High bounce risk.

**Jordan (Freelance Client)**: Looking for editorial or illustration specifically. The timeline mixes all categories with no filter. Has to scroll through motion work to find illustration. Frustrated by lack of focus. "Coming soon" overlay on what appear to be real images signals incomplete work — may assume the designer doesn't have enough completed projects to show.

---

## Minor Observations

- `.row-content { display: flex; gap: var(--space-xl); flex: 1; padding-top: 6px; }` — defined in CSS but the `.row-content` div was removed from the HTML template. Dead code.
- Hover blur deepening (12px to 16px) is appropriate for placeholder treatment but the transition is slow enough (400ms) that it may feel like the image is loading rather than reacting to hover.
- The `row-image-link:hover .row-image-overlay` gradient shift (transparent 50% to 40%) is imperceptibly subtle. Either remove it or make it meaningful.
- No project variety indicator or category filter — for a 6-project portfolio this is not blocking, but it sets a pattern that won't scale.

---

## Questions to Consider

1. **Is the focal row mechanic intentional or inherited?** If it was an experiment, is it earning its keep? If not, removing it is the single highest-impact fix.

2. **What is "Motion Identity (2023)" doing at index 2?** Is it the best work or just the middle item? If it's not intentionally the featured work, the focal system is choosing an arbitrary row to highlight.

3. **Does the work need a timeline format?** The timeline creates visual structure at the cost of image real estate and introduces the year as a sorting mechanism. Does the year matter to the audience, or would a curated grid serve the work better?
