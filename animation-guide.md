# GeoVault Animation Guide

Every animation must earn its place. This is a professional tool reviewers use hundreds of times a day — motion that doesn't serve clarity or feedback is a cost, not a feature.

## Should this animate at all?

| Frequency | Decision |
|---|---|
| 100+ times/day (Cmd+K open/close, keyboard nav) | No animation. Ever. |
| Tens of times/day (hover states, list row selection) | Remove or drastically reduce |
| Occasional (modals, drawers, toasts, panel open) | Standard animation |
| Rare (contradiction resolved, report approved, onboarding) | Can add a touch of delight |

**Never animate keyboard-initiated actions.** They're repeated too often — animation makes the interface feel slower than it is.

## Purpose test

Every animation needs a clear "why":
- **Spatial consistency** — the Extraction Verification correction panel always slides from the same edge
- **State indication** — the processing stepper morphs between states, not an abrupt swap
- **Feedback** — a button scales down slightly on press to confirm the click registered
- **Preventing jarring changes** — a new contradiction card fades/slides in rather than popping into the list instantly

If the only reason is "it looks cool" and it's something seen often, don't animate it.

## Easing — use these exactly

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);      /* entering elements */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);  /* on-screen movement/morphing */
```

- Entering/exiting element → `ease-out`
- Moving/morphing on screen → `ease-in-out`
- Hover/color change → `ease`
- Constant motion (progress bar) → `linear`
- Never `ease-in` on a UI element — it delays the exact moment the user is watching most closely and feels sluggish.

## Durations

| Element | Duration |
|---|---|
| Button press feedback | 100-160ms |
| Tooltips, small popovers | 125-200ms |
| Dropdowns, selects | 150-250ms |
| Modals, drawers, side panels (verification panel, borehole detail) | 200-400ms |
| Rare/celebratory moments | can run longer |

Keep UI animations under 300ms as a default ceiling. Exit animations are always faster than enter animations (e.g. side panel opens 300ms ease-out, closes 180ms ease-out) — pressing/deciding can be a touch slower, release/response is always snappy.

## Stagger

When a list loads (document list, borehole list, audit trail entries, contradiction cards), stagger each item 30-80ms. Never longer — long delays make the interface feel slow. Stagger is decorative; never block interaction while it plays.

## Springs

Use `useSpring`/`useMotionValue` from Motion for anything tied to continuous input (drag, pointer position, the map's camera transitions) — never `useState` for continuous values, it re-renders the tree on every change and collapses on mobile.

## Accessibility

```css
@media (prefers-reduced-motion: reduce) {
  /* keep opacity and color transitions — they aid comprehension */
  /* remove all transform/position-based motion */
}
```

```css
@media (hover: hover) and (pointer: fine) {
  /* gate all hover-only effects here — touch devices fire false-positive hovers */
}
```

## Review checklist before shipping a screen

| Issue | Fix |
|---|---|
| `transition: all` | Specify exact properties: `transition: transform 200ms ease-out` |
| `scale(0)` entry | Start from `scale(0.95)` + `opacity: 0` |
| `ease-in` anywhere in UI | Switch to `ease-out` or the custom curve above |
| Animation on a keyboard-triggered action | Remove it entirely |
| Duration over 300ms on a UI element | Reduce to 150-250ms |
| Hover animation with no media query guard | Add `(hover: hover) and (pointer: fine)` |
| All list items appearing at once | Add 30-80ms stagger |
| Enter/exit using the same speed | Make exit faster than enter |
