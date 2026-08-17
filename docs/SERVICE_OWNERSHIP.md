# Service ownership

## Runtime request path

```text
SafeCart-PWA -> SafeCart-API -> SafeCart-AI
```

- PWA owns capture/upload UX and evidence presentation.
- API owns the public contract, validation, orchestration, and failure mapping.
- AI owns OCR, entity extraction, candidate retrieval, matching, calibration, and
  deterministic evidence generation.
- Deployment pins compatible versions and exposes only the required ports.

`SafeCart-ScrapingData` prepares source snapshots offline and is not part of this path.
Runtime services consume reviewed, immutable, checksummed artifacts.

## Repository decision rule

Only independently deployable components with distinct ownership and release lifecycles
receive repositories. Internal modules, shared schemas, and small utilities remain in
their owning service until proven reuse requires another boundary.
