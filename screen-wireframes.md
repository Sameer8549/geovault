# GeoVault Screen Wireframes (rough — refine during build)

## 1. Dashboard
One sentence: a calm overview a reviewer checks each morning — status at a glance, nothing to act on yet.
```
┌─────────────────────────────────────────────┐
│ GeoVault          [search/⌘K]      [profile] │
├─────────────────────────────────────────────┤
│ [Docs Processed] [Boreholes] [Pending] [Done]│  <- KPI row, count-up
├─────────────────────────────────────────────┤
│ Recent Activity              │ Quick Actions │
│ - ingestion, corrections     │ [Upload Doc]  │
│ - approvals                  │ [Ask a Qstn]  │
└─────────────────────────────────────────────┘
```

## 2. Document Ingestion
One sentence: drop files in, watch them move through a clear pipeline, never a blank wait.
```
┌─────────────────────────────────────────────┐
│  [  Drag files here or click to upload  ]    │
├─────────────────────────────────────────────┤
│ file_1.pdf   Queued → Parsing → Extracted ●  │
│ file_2.pdf   Queued → Parsing ●              │
└─────────────────────────────────────────────┘
```

## 3. Extraction Verification (centerpiece)
One sentence: trust is built by always showing the source next to the claim.
```
┌───────────────────┬───────────────────────┐
│                    │ Borehole ID: bh_0042  │
│  [scanned page     │ Depth: 12.5–18.2 m ●● │
│   image, zoomable] │ Lithology: Sandstone  │
│                    │ GCV: 4850  [confirm/  │
│                    │  correct + reason]    │
├───────────────────┴───────────────────────┤
│ Audit trail (collapsible): A.Sharma edited │
│ GCV 4700→4850, reason: scan_misread        │
└─────────────────────────────────────────────┘
```

## 4. Contradiction Detection (hero feature)
One sentence: two truths can't both be silently accepted — show both, let a human decide.
```
┌───────────────────┬───────────────────────┐
│ Version A (doc_001)│ Version B (doc_014)  │
│ page 4, Sep 10     │ page 2, Sep 22        │
│ GCV: 4850          │ GCV: 5120 (diff)      │
├───────────────────┴───────────────────────┤
│ [Accept A]  [Accept B]  [Flag for Expert]  │
└─────────────────────────────────────────────┘
```

## 5. 3D Borehole Map
One sentence: the map IS the data — column height and color tell the geological story.
```
┌─────────────────────────────────────────────┐
│ [metric: GCV ▾]              [legend, glass]│
│                                               │
│     ▮      ▮▮                                │
│   ▮   ▮  ▮    ▮      (3D columns on terrain) │
│                                               │
└─────────────────────────────────────────────┘
Click column → slide-in panel: full log + source doc link
```

## 6. RAG Query / Ask
One sentence: every answer carries its receipt.
```
┌─────────────────────────────────────────────┐
│ > What is the GCV near Talcher Seam III?     │
│                                               │
│ ┌───────────────────────────────────────┐   │
│ │ The latest approved figure is 5120...  │   │
│ │ [doc_014, p.2, Sep 22] ← expandable    │   │
│ └───────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

## 7. Topic/Analytics Dashboard (lighter build)
```
┌─────────────────────────────────────────────┐
│ [word cloud]    [Topic: Grievances — 42 docs]│
│                 [Topic: Env. Reports — 18]   │
└─────────────────────────────────────────────┘
```

## 8. Report Drafting Workspace
```
┌─────────────────────────────────────────────┐
│ Prompt: "Draft response on Seam III GCV..."  │
│ ┌───────────────────────────────────────┐   │
│ │ Draft text with inline citations [1][2]│   │
│ └───────────────────────────────────────┘   │
│ [Approve] [Request Changes] [Reject]  [PDF]  │
└─────────────────────────────────────────────┘
```
