# SafeCart Deployment

Primary setup and source-code entry point for SafeCart, a marketplace product identity
matching system for COMPFEST 18 AIC.

SafeCart compares information visible in a listing with a versioned BPOM record. It
does **not** determine physical authenticity, chemical safety, or legal liability.

## Repository map

| Repository | Responsibility | Runtime |
| --- | --- | --- |
| [SafeCart-PWA](https://github.com/SafeCart-Compfest/SafeCart-PWA) | Mobile-first user experience | Yes, after AI gate |
| [SafeCart-API](https://github.com/SafeCart-Compfest/SafeCart-API) | Public API and orchestration | Yes |
| [SafeCart-AI](https://github.com/SafeCart-Compfest/SafeCart-AI) | OCR, retrieval, matching, training, and private inference | Yes |
| [SafeCart-ScrapingData](https://github.com/SafeCart-Compfest/SafeCart-ScrapingData) | Offline source acquisition | No |
| `SafeCart-Deployment` | Pinned integration, setup guide, and verification files | Orchestrator |

API and AI source trees are Git submodules pinned to reviewed commits. They are not
floating copies of `main`.

## Current runnable scope

The initial composition validates the API-to-AI service boundary:

```text
client -> SafeCart-API :8000 -> SafeCart-AI :8001 (private network)
```

The PWA is intentionally excluded until the AI required checks pass. The current
bootstrap provides health and readiness checks; it is not yet the final assessment MVP.

## Prerequisites

- Git 2.40 or newer.
- Docker Engine 24+ with Compose v2.
- At least 4 GB free memory for the bootstrap services. Final model requirements will
  be documented after the CPU model file is finalized.

## Setup

Clone with pinned service sources:

```bash
git clone --recurse-submodules https://github.com/SafeCart-Compfest/SafeCart-Deployment.git
cd SafeCart-Deployment
docker compose up --build
```

If the repository was cloned without submodules:

```bash
git submodule update --init --recursive
```

Verify the running boundary in another terminal:

```bash
curl http://localhost:8000/health
curl http://localhost:8000/ready
```

Expected readiness response:

```json
{"status":"ready","dependencies":{"ai":"ok"}}
```

Stop the stack with `docker compose down`. The bootstrap does not persist uploads,
datasets, or model output.

## Reproducibility rules

- Update a service pin only through a pull request after that service's CI is green.
- Record the service PR and evaluation impact in the deployment PR.
- Never point Compose at an unpinned branch or run scraping during evaluation.
- Keep raw datasets, private screenshots, credentials, and model weights outside Git.
- Mark the final submission with an immutable `preliminary-2026` tag only after the clean
  clone checklist passes.

See `docs/SERVICE_OWNERSHIP.md` and `docs/SUBMISSION_CHECKLIST.md` for the integration
contract and final audit.
