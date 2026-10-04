# GeoVault Design Principles

Approach this as a design studio lead who gives every client a distinct identity. This client has already rejected templated proposals — make deliberate, opinionated choices specific to this brief.

## Ground the design in the subject matter

GeoVault's world: boreholes, lithology intervals, seam thickness, GCV/ash/moisture readings, scanned geological reports, parliamentary reporting workflows. The audience is technical reviewers and administrative officers, not consumers. Every visual choice should come from that vernacular, not a generic SaaS template.

## Plan before building

1. **Color** — four to six named tokens with a role each (locked in `design-tokens.css`, do not deviate).
2. **Type** — Cabinet Grotesk (display) / Inter (body/UI) / JetBrains Mono (IDs, coordinates, technical values). State which one carries personality — it's the display face, used sparingly on section headers and KPI numbers.
3. **Layout** — describe each major screen in one sentence plus an ASCII wireframe before building it (see `screen-wireframes.md`). Decide alignment per screen deliberately — data tables and forms left-align, KPI/stat displays can center.
4. **Principles** — what makes GeoVault distinct from a generic admin dashboard: every value on screen can be traced to its source page, and that traceability is visually built in (inline citation chips, source-page thumbnails), not an afterthought link.

## Anti-default discipline — avoid these generated-UI tells

- Warm cream background (~#F4F1EA) with high-contrast serif + terracotta accent
- Near-black background with a single acid-green/vermilion accent
- Broadsheet layout with hairline rules and zero border-radius everywhere
- The SaaS-card kit: identical rounded cards, one border-radius regardless of hierarchy, identical soft grey shadow, gradient washes as decoration
- Tracked-out ALL-CAPS eyebrow labels above every heading
- Meta strings joined with middle dots ("A · B · C")
- A monospace face used for every small label regardless of whether it's actually technical data
- "→" appended to every link/button
- Accenting a single word in a headline via color/italic/bold
- Numbered markers (01/02/03) when the content isn't actually a sequence

All of these are legitimate for *some* brief — they're banned here because they don't serve this one. Where this brief specifies something explicitly (e.g. JetBrains Mono for coordinates), that wins.

## Restraint

Spend boldness in exactly one place per screen:
- Extraction Verification → the confidence-bar visualization
- Contradiction Detection → the diff highlight
- 3D Borehole Map → the column height/color encoding

Everything surrounding the bold element stays quiet and disciplined. Cut any decoration that doesn't serve comprehension. Build to a quality floor without announcing it: responsive to mobile (reviewers may check status on a phone), visible keyboard focus, reduced motion respected, accessible contrast, harmonious palette (the token set already ensures this).

Self-critique after every screen: screenshot it, ask "does this look like any other AI-generated admin dashboard?" If yes, remove one decorative element and recheck.

## Writing in the interface

Words exist to make the interface easier to understand and use — they are content, not decoration.

- Write from the reviewer's perspective, in plain language they'd use, not system/implementation terms. "Needs Review," not "Pending Validation Queue."
- Active voice, exact outcomes: a button labeled "Approve Report" produces a confirmation that says "Report approved" — the vocabulary stays identical through the whole flow.
- Empty and error states explain what happened and what to do next, in the interface's own calm voice — never apologetic, never vague. "No supporting evidence found in corpus" — not "Oops, nothing here!"
- Sentence case throughout, no filler words, each label doing exactly one job.
