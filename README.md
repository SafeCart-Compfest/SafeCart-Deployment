# SafeCart Deployment

Primary setup and source-code entry point for SafeCart, a marketplace product identity
matching system for COMPFEST 18 AIC.

SafeCart compares information visible in a listing with a versioned BPOM record. It
does **not** determine physical authenticity, chemical safety, or legal liability.

## Repository map

| Repository | Responsibility | Status |
| --- | --- | --- |
| [SafeCart-PWA](https://github.com/SafeCart-Compfest/SafeCart-PWA) | Mobile-first frontend | Not integrated |
| [SafeCart-API](https://github.com/SafeCart-Compfest/SafeCart-API) | Public API and orchestration | Available |
| [SafeCart-AI](https://github.com/SafeCart-Compfest/SafeCart-AI) | OCR, retrieval, matching, and training | Available |
| [SafeCart-ScrapingData](https://github.com/SafeCart-Compfest/SafeCart-ScrapingData) | Offline data collection | Not a runtime service |
| `SafeCart-Deployment` | Docker Compose setup | Available |

API and AI source trees are Git submodules pinned to reviewed commits. They are not
floating copies of `main`.

## Current runnable scope

The initial composition validates the API-to-AI service boundary:

```text
client -> SafeCart-API :8000 -> SafeCart-AI :8001 (private network)
```

The PWA is not included in the current Compose setup.

## Prerequisites

- Git 2.40 or newer.
- Docker Engine 24+ with Compose v2.
- At least 4 GB free memory.

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

Stop the stack with `docker compose down`. The services do not persist uploads,
datasets, or model output.
