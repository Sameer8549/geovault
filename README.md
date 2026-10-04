# GeoVault

AI-powered geological document intelligence and reporting platform for CMPDI/Coal India (SIH 2026 prototype).

This README is also the build prompt for Antigravity — point it at this repo and `docs/` to generate the frontend.

---

## Design Read

> Reading this as: enterprise government geological-data product for technical/administrative reviewers — a dense data product, not a landing page — with a precise, trust-first data language, leaning toward shadcn/ui + Tailwind v4 + restrained, purposeful motion.

**Dials for this build** (dashboard/product UI, not marketing):
- `DESIGN_VARIANCE: 4` — government/trust-first data product; order and predictability matter more than visual flair
- `MOTION_INTENSITY: 3` — reviewers use this hundreds of times a day; motion must never slow them down
- `VISUAL_DENSITY: 5` — a data-dense professional tool, not an art-gallery layout

See `docs/design-principles.md` and `docs/animation-guide.md` for the full rule set — read both before writing any UI code.

---

## Stack — Dynamic Edition (supersedes earlier Next.js version)

- Vite + React 19 + TypeScript, React Router v7
- Tailwind CSS v4
- shadcn/ui — fully restyled for Ethereal Glass, never shipped default
- Motion (`motion/react`) for component micro-interactions
- GSAP + ScrollTrigger for cinematic scroll-driven section entrances
- Lenis for smooth scroll (drives all scroll-based motion)
- Mapbox GL JS v3 + deck.gl 9.x (3D borehole columns)
- Three.js — subtle ambient background layer, dashboard shell only
- Recharts, TanStack Query, Zod
- Phosphor Icons (Light weight) — NOT lucide-react
- Fonts: Clash Display (display) + Plus Jakarta Sans (body) + JetBrains Mono (technical values) — NOT Inter
- pnpm

Visual direction: **Ethereal Glass** (OLED black, glowing mesh gradients, glass cards) + **Z-Axis Cascade** layout for Dashboard/Contradiction Detection. Full rules in `docs/design-principles.md` and `docs/animation-guide.md` — these are binding, not suggestions.

---

## Information architecture — 8 screens

1. **Dashboard** — KPI row (animated count-up), recent activity feed, quick-access CTAs
2. **Document Ingestion** — drag-and-drop upload, animated processing stepper (Queued → Parsing → Extracted → Needs Review → Verified)
3. **Extraction Verification** (centerpiece) — split view: source page image (zoomable) left, structured fields with confidence bars right, reason-coded corrections logged to an audit trail
4. **Contradiction Detection** (hero/differentiator) — side-by-side version comparison when two documents disagree on the same borehole_id + depth interval; one-click resolve (Accept A / Accept B / Flag for expert review)
5. **3D Borehole Map** — Mapbox base + deck.gl ColumnLayer, height = depth, color = selectable metric (GCV/ash/confidence), click-to-open lithology log panel
6. **RAG Query / Ask** — chat interface, answers as cards with expandable citation chips, explicit calm "not found in corpus" state
7. **Topic/Analytics Dashboard** (lighter build) — word cloud + topic clusters, click to filter documents
8. **Report Drafting Workspace** — prompt → cited draft → Approve/Request Changes/Reject → PDF export stamped with reviewer + timestamp

Full wireframe sketches: `docs/screen-wireframes.md`
API shapes to build mock data against: `docs/api-contract.md`
Domain terminology source: `docs/source-blueprint.pdf`

---

## Design tokens

Use `docs/design-tokens.css` verbatim in `app/globals.css`. Do not introduce any color outside this token set — every component references tokens via Tailwind utilities (`bg-surface`, `text-text-primary`, `border-border`, etc.), never a hardcoded hex/oklch value inline.

---

## Anti-default discipline — banned outright

- Warm cream (#F4F1EA) + terracotta accent, or near-black + single acid accent
- Identical rounded cards with the same soft grey shadow + gradient wash
- Tracked-out ALL-CAPS eyebrow labels above every heading
- Numbered markers (01/02/03) unless content is a genuine sequence
- "→" appended to every button/link
- Fade-and-slide-up on every section — reserve ONE orchestrated motion moment per screen
- AI-purple gradients, generic glassmorphism on everything, infinite-loop micro-animations

**Restraint rule:** one bold visual element per screen, everything else disciplined.
- Extraction Verification → the confidence-bar visualization
- Contradiction Detection → the diff highlight
- 3D Borehole Map → the column height/color encoding

---

## Copy rule

Write every label from the reviewer's perspective in plain language. Buttons say exactly what happens: "Approve Report," not "Submit." Empty/error states explain what happened and what to do next, in the interface's voice, never apologetic: "No supporting evidence found in corpus" — not "Oops, nothing here!"

---

## Self-critique pass

After building each screen, screenshot it and ask: "does this look like any other AI-generated admin dashboard?" If yes, remove one decorative element and recheck before moving to the next screen.

---

## Deliverable

Full working Next.js 16.3 app named **GeoVault** throughout (page titles, nav branding, favicon placeholder), mock data from `mock-data/` wired into all 8 screens, clear `// TODO: replace with real Fly.io/Supabase endpoint` markers matching `docs/api-contract.md`, and this README's rules followed exactly — confirm compliance in your final summary.

---

## Backend (reference, not built by this repo)

- FastAPI on Fly.io
- Supabase Postgres with PostGIS (spatial) + pgvector (RAG embeddings) extensions
- NVIDIA Nemotron/NIM as primary vision/extraction model, Groq as fast fallback
- Vercel for this frontend's deployment
