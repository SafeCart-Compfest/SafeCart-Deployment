# Contributing

`main` is protected. Every change uses a short-lived branch, Conventional Commit,
pull request, green checks, documented self-review, and squash merge.

For service pin updates:

1. Merge and verify the source-service pull request.
2. Update only the relevant submodule pointer.
3. Explain compatibility and evaluation impact in the deployment pull request.
4. Run the Compose configuration and clean-clone smoke checks.

Never force-push, merge locally into `main`, or commit credentials, raw data, private
screenshots, generated artifacts, or model weights.
