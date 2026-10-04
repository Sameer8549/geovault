# GeoVault — Hard Rules (always apply) — Dynamic Edition

(Supersedes any earlier Next.js / restrained-dashboard version of this file.)

## Stack lock
Vite + React 19 + TypeScript + React Router v7, Tailwind CSS v4, shadcn/ui
(restyled, not default), Motion (`motion/react`), GSAP + ScrollTrigger, Lenis
smooth scroll, Mapbox GL JS v3 + deck.gl 9.x, optional Three.js ambient
background (dashboard shell only), Recharts, TanStack Query, Zod, Phosphor
Icons (Light weight only), pnpm.

NO Next.js. NO lucide-react. NO Inter/Roboto/Arial/Helvetica.

## Vibe + Layout archetypes (locked)
- Vibe: Ethereal Glass — OLED black (#050505), glowing off-center mesh
  gradients (electric blue + emerald), glass cards with backdrop-blur-2xl
  and white/8% hairline borders
- Layout: Z-Axis Cascade for Dashboard + Contradiction Detection (overlapping
  cards, -2deg to 3deg rotation, collapses flat below 768px)

## Banned outright
- Inter, Roboto, Arial, Open Sans, Helvetica
- Default lucide / FontAwesome / Material Icons (thick-stroke) — Phosphor
  Light only
- Generic 1px solid gray borders; harsh flat drop shadows
- Edge-to-edge sticky navbar glued to top — floating detached glass pill
  nav only
- Symmetric boring grids with no whitespace drama
- Default `linear`/`ease-in-out` transitions — custom cubic-bezier only
- Static appearance with no entrance animation
- White/light background as the default surface anywhere
- Any color not defined in docs/design-tokens.css

## Animation hard limits
- Lenis drives all scroll; GSAP ScrollTrigger for section entrances; Motion
  for component-level micro-interactions and shared-element transitions
- ease-fluid: cubic-bezier(0.32, 0.72, 0, 1) — primary UI motion
- ease-out: cubic-bezier(0.23, 1, 0.32, 1) — entrances
- ease-in-out: cubic-bezier(0.77, 0, 0.175, 1) — on-screen movement
- Never ease-in on a UI element
- Durations: button feedback 100-160ms, tooltips 125-200ms, dropdowns
  150-250ms, modals/drawers 200-400ms, scroll entrances 700-900ms
- Exit animations always faster than enter animations
- List stagger 30-80ms per item
- Cmd/Ctrl+K: zero delay on keypress detection, only the resulting modal
  animates
- Animate only transform/opacity — never top/left/width/height
- Respect prefers-reduced-motion and (hover: hover) and (pointer: fine)

## Component requirements
- Double-Bezel nested architecture on all major cards (outer shell + inner
  core, concentric radii)
- Island buttons: rounded-full pills, trailing icon nested in its own
  circular wrapper, never bare
- Magnetic hover physics on primary CTAs (scale + nested icon translate)
- Section padding minimum py-24

## Information legibility (still mandatory in a dynamic build)
Confidence bars, contradiction diff highlights, and the 3D map's
height/color encoding must stay clearly readable at a glance inside the
glowing/animated shell. Motion serves the data, never buries it.

## Naming
Product name is "GeoVault" everywhere. No logo graphic — the wordmark set
in Clash Display IS the brand mark.

Full rationale: docs/design-principles.md and docs/animation-guide.md.
