# GeoVault API Contract (reference for mock data + future backend wiring)

Base URL (future): `https://geovault-backend.fly.dev`
Frontend uses mock data matching these shapes until the real backend exists.

## GET /documents
Returns list of ingested documents.
```json
{
  "documents": [
    {
      "id": "doc_001",
      "title": "Borehole Log — Talcher Coalfield Sector 4",
      "category": "borehole_log",
      "status": "verified",
      "uploaded_at": "2026-09-10T08:30:00Z",
      "page_count": 12,
      "confidentiality": "internal"
    }
  ]
}
```

## GET /documents/{id}
Full document detail with page images and extraction status per page.

## POST /documents/upload
Multipart upload. Returns `{ "document_id": "...", "status": "queued" }`.

## GET /boreholes
```json
{
  "boreholes": [
    {
      "id": "bh_0042",
      "report_id": "doc_001",
      "latitude": 21.0045,
      "longitude": 85.2201,
      "geometry": "POINT(85.2201 21.0045)",
      "intervals": [
        {
          "from_depth": 12.5,
          "to_depth": 18.2,
          "lithology": "Sandstone, fine-grained",
          "seam_name": "Seam III",
          "ash_pct": 18.4,
          "gcv": 4850,
          "moisture_pct": 6.1,
          "source_page": 4,
          "confidence": 0.91
        }
      ]
    }
  ]
}
```

## GET /boreholes/{id}
Full lithology log for one borehole with source page references.

## GET /contradictions
```json
{
  "contradictions": [
    {
      "id": "conf_001",
      "borehole_id": "bh_0042",
      "field": "gcv",
      "depth_interval": "12.5-18.2",
      "version_a": { "document_id": "doc_001", "page": 4, "value": 4850, "date": "2026-09-10" },
      "version_b": { "document_id": "doc_014", "page": 2, "value": 5120, "date": "2026-09-22" },
      "status": "unresolved"
    }
  ]
}
```

## POST /contradictions/{id}/resolve
```json
{ "resolution": "accept_a" | "accept_b" | "flag_expert_review", "reviewer": "string", "note": "string" }
```

## POST /ask
```json
// request
{ "question": "What is the latest approved GCV for Seam III near Talcher?" }

// response
{
  "answer": "The latest approved GCV figure is...",
  "citations": [
    { "document_id": "doc_014", "page": 2, "excerpt": "...", "date": "2026-09-22" }
  ],
  "grounded": true
}
// grounded: false + no citations => render the "not found in corpus" state
```

## GET /reports/{id} , POST /reports/draft , POST /reports/{id}/approve
Draft generation, approval workflow, and PDF export — same citation shape as /ask.

## GET /audit-log?target_id=...
```json
{
  "entries": [
    {
      "field": "gcv",
      "before": 4700,
      "after": 4850,
      "reviewer": "A. Sharma",
      "reason_code": "scan_misread",
      "timestamp": "2026-09-11T10:02:00Z"
    }
  ]
}
```
