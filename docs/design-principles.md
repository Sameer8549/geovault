# GeoVault Design Principles — Dynamic / Ethereal Glass Edition

(Supersedes the earlier restrained-dashboard version. This is now a $150k-agency-tier dynamic experience, not a quiet government admin panel.)

## Persona
You are building as a Vanguard UI Architect — the output must exude haptic depth, cinematic spatial rhythm, obsessive micro-interactions, and flawless fluid motion. Never generate the same layout/aesthetic twice across screens — vary within the locked archetype below.

## Vibe Archetype: Ethereal Glass (locked for this project)
Deepest OLED black background (`#050505`). Subtle radial glowing mesh gradients in the background — electric blue + emerald, low opacity, positioned off-center, never centered/symmetrical. Vantablack glass cards with heavy `backdrop-blur-2xl` and white/8% hairline borders. Wide geometric display typography for headers.

## Layout Archetype: Z-Axis Cascade
Elements stacked like physical cards, slightly overlapping with varying depth, some with a subtle -2deg to 3deg rotation to break the digital grid. Used especially on Dashboard and Contradiction Detection. Collapses to a clean vertical stack with zero rotation below 768px — overlapping elements cause touch-target conflicts on mobile, so remove all rotation and negative-margin overlap there.

## Absolute-zero banned list (instant fail if present)
- Fonts: Inter, Roboto, Arial, Open Sans, Helvetica
- Icons: default lucide, FontAwesome, Material Icons (thick-stroke). Use Phosphor Light only.
- Generic 1px solid gray borders; harsh dark drop shadows (`shadow-md`, `rgba(0,0,0,0.3)`)
- Edge-to-edge sticky navbar glued to the top — use a floating detached glass pill nav instead
- Symmetric boring grids with no whitespace drama
- Any default `linear`/`ease-in-out` transition — custom cubic-bezier only
- Elements appearing statically with no entrance animation
- White/light background as the default surface anywhere in the app

## Component mastery

**Double-Bezel (nested architecture)** — never place a card flatly on the background:
- Outer shell: wrapper div, subtle bg (`bg-white/5`), hairline ring (`ring-1 ring-white/5`), padding `p-1.5`-`p-2`, large radius `rounded-[2rem]`
- Inner core: distinct background, inner highlight (`shadow-[inset_0_1px_1px_rgba(255,255,255,0.15)]`), smaller concentric radius

**Island buttons** — primary CTAs are fully rounded pills (`rounded-full`, `px-6 py-3`). A trailing icon never sits naked — nest it in its own circular wrapper (`w-8 h-8 rounded-full bg-white/10`), flush with the button's inner padding.

**Spatial rhythm** — double standard padding, `py-24` to `py-40` on major sections. Eyebrow tags before H1/H2s are a microscopic pill badge (`rounded-full px-3 py-1 text-[10px] uppercase tracking-[0.2em]`) - use sparingly, not on every heading.

## Performance guardrails (non-negotiable)
- Animate only `transform` and `opacity` — never `top`, `left`, `width`, `height`
- `backdrop-blur` only on fixed/sticky elements (nav, overlays) — never on scrolling content or large containers
- Any grain/noise texture goes on a `fixed`, `pointer-events-none` layer, never attached to scrolling containers
- No arbitrary `z-50`/`z-[9999]` — reserve z-index values strictly for systemic layers

## Restraint still applies, differently here
This isn't "one bold element per screen" anymore — it's "every screen gets the full Ethereal Glass treatment," but the *information itself* stays legible: confidence bars, diff highlights, and the 3D map encoding still need to read clearly at a glance even inside a glowing, animated shell. Motion serves the data, never buries it.

## Copy voice (unchanged)
Write every label from the reviewer's perspective, plain language. Buttons say exactly what happens: "Approve Report," not "Submit." Empty/error states explain what happened and what to do, in the interface's calm voice — "No supporting evidence found in corpus," not "Oops, nothing here!"

## Pre-output checklist (run before shipping each screen)
- [ ] No banned font/icon/border/shadow/layout/motion present
- [ ] Vibe (Ethereal Glass) and Layout (Z-Axis Cascade where applicable) consciously applied
- [ ] Major cards use Double-Bezel nested architecture
- [ ] CTAs use island/button-in-button pattern where applicable
- [ ] Section padding at minimum py-24
- [ ] All transitions use custom cubic-bezier, never linear/ease-in-out
- [ ] Scroll entry animations present on every section
- [ ] Layout collapses cleanly below 768px
- [ ] Only transform/opacity animated
- [ ] backdrop-blur only on fixed/sticky elements
- [ ] Reads as a $150k agency build, not a template with nice fonts
