# GeoVault Animation Guide — Dynamic Edition

Two layers of motion now: (1) Motion (`motion/react`) for component-level micro-interactions, and (2) GSAP + ScrollTrigger + Lenis for cinematic, scroll-driven choreography across the page. Use the right tool for each job — don't reach for GSAP on a simple hover state, and don't try to build scroll-pinning with Motion alone.

## Smooth scroll — Lenis
Initialize Lenis once at the app root. All scroll-triggered animation (GSAP ScrollTrigger, Motion's `whileInView`) must read scroll position through Lenis, not the native scroll event, so motion stays buttery and frame-synced.

## Scroll entry animations — GSAP ScrollTrigger
Elements never appear statically on load or on scroll into view. Default entrance:
```
translateY(16px) + blur(8px) + opacity:0  →  translateY(0) + blur(0) + opacity:1
duration: 800ms+, custom cubic-bezier (see easing below)
```
Use `IntersectionObserver`-backed triggers (ScrollTrigger handles this internally) — never raw `window.addEventListener('scroll')`, which causes reflows and kills mobile performance.

## Component micro-interactions — Motion
Use Motion for anything tied to component state: button press, panel open/close, list stagger, shared-element transitions (`layoutId`) between a row and its detail view (contradiction cards, borehole click, document open).

## Easing — custom cubic-beziers only, never default
```css
--ease-fluid: cubic-bezier(0.32, 0.72, 0, 1);     /* primary UI motion */
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);        /* entrances */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);    /* on-screen movement */
```
Never `linear` or default `ease-in-out` from the browser. Never `ease-in` on a UI element — it delays feedback at the exact moment attention is highest.

## Durations
| Element | Duration |
|---|---|
| Button press feedback | 100-160ms |
| Tooltips, small popovers | 125-200ms |
| Dropdowns, selects | 150-250ms |
| Modals, drawers, side panels | 200-400ms |
| Scroll-triggered section entrance | 700-900ms |
| Hamburger/nav morph | 400-600ms with staggered child reveal |

Exit animations are always faster than enter animations.

## Signature choreography patterns (required)

**Fluid Island nav**: floating glass pill nav, detached from the top edge (`mt-6 mx-auto w-max rounded-full`). Hamburger (if used on mobile) morphs its lines into an X via rotate/translate, never a disappear/reappear swap. Expanded menu overlay uses `backdrop-blur-3xl bg-black/80`, nav links reveal with staggered mask (`translateY(12px) opacity:0` → `translateY(0) opacity:1`, 50-80ms stagger per item).

**Magnetic button hover**: on hover, scale the whole button down slightly (`active:scale-[0.98]`) to simulate a physical press. A nested icon circle translates diagonally and scales up slightly on hover, creating internal kinetic tension — never just a flat background color change.

**List stagger**: document list, borehole list, audit trail entries, contradiction cards — stagger 30-80ms per item on mount, never longer.

## Keyboard-triggered actions
Cmd/Ctrl+K command palette: the trigger itself has zero animation delay (instant response to the keystroke) — only the resulting modal expansion animates (glass-blur expand, 200-300ms). Never animate the detection of the keypress itself.

## Accessibility — still mandatory in a dynamic build
```css
@media (prefers-reduced-motion: reduce) {
  /* keep opacity/color transitions, remove all transform/position/blur motion */
}
@media (hover: hover) and (pointer: fine) {
  /* gate all hover-only effects here */
}
```

## Performance rules (non-negotiable even with heavier motion)
- Animate only `transform` and `opacity` — never layout-triggering properties (`top`, `left`, `width`, `height`)
- `will-change: transform` sparingly, only on actively-animating elements
- `backdrop-blur` only on fixed/sticky elements, never on scrolling containers
- Three.js ambient background layer (dashboard shell only): low particle count, capped frame budget, pause/reduce when tab is backgrounded

## Review checklist before shipping a screen
- [ ] No `transition: all` — exact properties specified
- [ ] No default `ease-in-out`/`linear` anywhere
- [ ] Every section has a scroll-entry animation
- [ ] List stagger present and under 80ms per item
- [ ] Enter animations slower than exit animations
- [ ] Keyboard-triggered actions have zero input-detection delay
- [ ] prefers-reduced-motion and hover media query guards present
- [ ] Only transform/opacity animated anywhere in the codebase
