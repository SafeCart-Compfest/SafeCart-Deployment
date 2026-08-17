## Summary

- What integration or pinned service version changes?
- Why is the change required?

## Validation

- [ ] Referenced service CI is green.
- [ ] `docker compose config --quiet` passes.
- [ ] Clean-clone `docker compose up --build` passes when Docker is available.
- [ ] `/health` and `/ready` return the documented responses.

## Safety and reproducibility

- [ ] Submodules point to reviewed immutable commits.
- [ ] No secret, raw dataset, private screenshot, model weight, or generated output is included.
- [ ] README and submission evidence remain accurate.
