# Shape — /work page: Cinemascope Redesign

## Intent

Transform the /work page from a timeline list into a full-viewport editorial
presentation. Each project occupies the full viewport height, centered in a 4:3
content frame (letterboxed on 16:9 viewports). The viewer scrolls through
projects with snap-stop, like turning pages of a book — the current project
fills the frame; adjacent projects peek at top/bottom edges at 10% opacity.

This is a **curated spotlight**, not a list. The work dominates.

---

## Layout Architecture

### Viewport math

```
Viewport:    16:9   (e.g. 1440 × 810)
Content:     4:3    (e.g.  960 × 720)
Letterbox:  (810 - 720) / 2 = 45px top + 45px bottom
```

### CSS Structure

```
.page-work
  └── .timeline          ← full viewport height, scroll container, snap-y mandatory
       └── .timeline-row ← 100vh each, scroll-snap-align: center
            ├── .row-frame   ← 4:3 aspect ratio, centered, max 960×720
            │    ├── .row-image-wrap
            │    └── .row-meta
            └── .row-bubble  ← year bubble, positioned in the letterbox margin
```

### Scroll behavior

- `scroll-snap-type: y mandatory` on `.timeline`
- Each `.timeline-row` is `height: 100vh`, `scroll-snap-align: center`
- The row's content (`.row-frame`) is `aspect-ratio: 4/3`, max-width constrained
  to fit inside the 4:3 on the current viewport
- Adjacent rows are naturally visible at top/bottom (they take 100vh each)
- Focal row detected via IntersectionObserver with threshold ~0.5

### Focal mechanic

- Rows start at `opacity: 0.10` (near-invisible, still fully in DOM)
- When a row's center is within the viewport center zone, it becomes the
  focal row: `opacity: 1`
- Adjacent rows (previous/next in DOM order) visible at 0.10 in the margins
- No middle-row assumption — any row can be the focal row based on scroll

---

## Content Split per Row

### Alternating pattern

- `row-image-left`:  [IMAGE — left half of frame] | [META — right half]
- `row-image-right`: [META — left half] | [IMAGE — right half]

Both sides stay within the 4:3 frame — no content bleeds outside.

### Focal row proportions

Within the 4:3 frame:
- Image: `60%` of frame width (not full width — leaves room for meta on one side)
- Meta: `40%` of frame width, stacked vertically in its half

This is a wide editorial spread, not a card.

### Non-focal rows (adjacent, opacity 0.10)

- Same proportions
- Visible as a thin sliver at top/bottom edge
- The opacity is low enough that they feel like "page edges" peeking into view

---

## Focal Row Meta Treatment

The meta column within the focal row should feel editorial:

```
[Category label — small caps, primary color, top]
[Title — large, bold, neutral-text]
[Description — 2–3 lines, muted, comfortable size]
[Year — bottom right, small]
```

Size relationships within the 4:3 frame at ~960px wide:
- Title: ~28–32px
- Description: ~14–16px
- Category: ~11px uppercase

---

## Year Bubble Repositioning

Currently the bubble sits at the top of the row content. In cinemascope:

- The bubble should sit in the **letterbox margin** — the space above or below
  the 4:3 frame on a 16:9 viewport
- This puts the year "outside" the content frame, like a film reel marker
- `position: fixed` relative to the viewport with a transform to place it in
  the top or bottom letterbox depending on focal row position

Or more simply: the bubble is absolutely positioned within `.timeline-row`
(100vh), not within `.row-frame`. Since `.row-frame` is 4:3 and centered
vertically in the 100vh row, the bubble can sit at `top: calc((100vh - 4/3 * 60vw) / 2 - 22px)` — the letterbox space.

Simplest approach: `.row-bubble` is `position: absolute` on `.timeline-row`,
vertically centered on the row, `left: 50%` (centered horizontally on the page).

---

## Responsive Strategy

### Below 1024px

Collapse to single-column. The 4:3 framing no longer applies — each row
stacks image above meta, full-width. Scroll-snap becomes optional or disabled.
Adjacent rows fade at 0.10 as before.

### Mobile (< 768px)

No scroll-snap (too janky on touch). Full vertical list. Images full-width.
Meta below. All rows at opacity 1 (no focal mechanic). Timeline rule on left
edge. Minimal chrome.

---

## Animation

- **Entrance**: When a row becomes focal (opacity 0.10 → 1), the content
  inside the frame does a subtle `scale(0.98) → scale(1)` + `opacity` transition,
  ~400ms ease-out-quart. Cinematic, not bouncy.
- **Exit**: Scale to 1.02 as it fades back to 0.10, then reset to 1 for next use.
- **Hover on focal row image**: subtle scale to 1.02, 300ms ease-out.
- **No stagger** — the focal row is the only one with entrance animation.
- `prefers-reduced-motion`: all transitions instant, opacity fade disabled.

---

## Visual Refinements

1. Remove `.page-header` entirely from the work page. The cinemascope experience
   has no preamble — you land on the first project.
2. The "Work" title could live as a small fixed watermark at top-left of
   the viewport, or as the browser tab title.
3. The `.row-frame` needs a subtle border or shadow to define its edges
   against the letterbox space.
4. The timeline vertical rule (`.timeline::before`) is **removed** — the
   letterbox negative space replaces it as the visual separator.

---

## Data Model

No changes to the `projects` array. The `slug`, `title`, `category`, `year`,
`description`, and `image` fields are all used. An additional `featured: true`
flag could be added later to force a specific row to start in focus on load.

---

## Scope for Implementation

### Phase 1 (this pass)
- CSS structural rewrite: 100vh rows, scroll-snap, 4:3 frame, letterboxing
- Focal row observer: any row at 0.5+ threshold → opacity 1, others → 0.10
- Remove dead CSS (`.row-left/.row-right`, `.row-content`)
- Alternating L/R within the 4:3 frame
- Year bubble repositioned to letterbox margin
- Responsive collapse below 1024px

### Phase 2 (follow-up)
- Content scale and type size refinement within 4:3 frame
- Entrance animation for focal rows
- Mobile full vertical list
- Project counter ("03 / 06")
