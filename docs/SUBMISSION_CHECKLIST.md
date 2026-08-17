# Preliminary submission checklist

Do not create the final tag until every applicable item is complete.

## Repository

- [ ] All component repositories are public and linked from the root README.
- [ ] Protected branches, required checks, squash-only merges, and secret scanning are enabled.
- [ ] Submodules point to reviewed commits and initialize from a clean clone.
- [ ] No pending changes exist in any submitted repository.

## AI evidence

- [ ] Frozen test set was not used for model or threshold selection.
- [ ] Baselines and fine-tuned model use the same split and evaluation contract.
- [ ] Acceptance metrics include bootstrap confidence intervals and error analysis.
- [ ] Data manifest, model card, artifact version, and SHA-256 are published.
- [ ] Ambiguous and low-evidence cases abstain.

## Runtime

- [ ] `docker compose up --build` succeeds on a clean machine.
- [ ] Health, readiness, upload validation, and golden assessment cases pass.
- [ ] Uploaded screenshots are processed in memory and are not persisted.
- [ ] CPU p95 latency is measured on documented hardware.

## Submission

- [ ] Proposal claims match measured evidence and include the non-claim disclaimer.
- [ ] Demo and promotional assets contain no prohibited institution branding.
- [ ] The immutable `preliminary-2026` tag points to the audited deployment commit.
- [ ] Submission is completed before the deadline buffer.
