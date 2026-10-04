# GeoVault — Hard Rules (always apply)

## Dials
- DESIGN_VARIANCE: 4
- MOTION_INTENSITY: 3
- VISUAL_DENSITY: 5

## Banned outright
- Warm cream (#F4F1EA) + terracotta accent, or near-black + single acid accent
- Identical rounded cards with identical soft grey shadow + gradient wash
- Tracked-out ALL-CAPS eyebrow labels above headings
- Numbered markers (01/02/03) unless content is a genuine sequence
- "→" appended to button/link text
- Fade-and-slide-up entrance on every section (max one orchestrated motion moment per screen)
- AI-purple gradients, blanket glassmorphism, infinite-loop micro-animations
- Any color not defined in docs/design-tokens.css

## Animation hard limits
- Never animate keyboard-triggered actions (Cmd+K instant, no transition)
- ease-out: cubic-bezier(0.23, 1, 0.32, 1) for entering elements
- ease-in-out: cubic-bezier(0.77, 0, 0.175, 1) for on-screen movement
- Never use ease-in on UI elements
- Durations: button feedback 100-160ms, tooltips/popovers 125-200ms, dropdowns 150-250ms, modals/drawers 200-400ms
- Exit animations always faster than enter animations
- List items stagger 30-80ms, never longer
- Respect prefers-reduced-motion (keep opacity/color, drop transform/position)
- Gate hover effects behind (hover: hover) and (pointer: fine)

## One bold element per screen
- Extraction Verification → confidence-bar visualization
- Contradiction Detection → diff highlight
- 3D Borehole Map → column height/color encoding
Everything else on that screen stays quiet.

## Stack lock
Next.js 16.3, React 19.2, TypeScript 5.9, Tailwind v4, shadcn/ui, Motion (`motion/react`), Mapbox GL JS v3 + deck.gl 9.x, Recharts, TanStack Query, Zod, next-themes, lucide-react, pnpm.

## Naming
Product name is "GeoVault" everywhere — page titles, nav, favicon, metadata. Never "GeoSense" or any other prior working name.

Full rationale for every rule above: see docs/design-principles.md and docs/animation-guide.md in this repo.
