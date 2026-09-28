# Claude Code Instructions

Follow the workflow defined in [AGENTS.md](AGENTS.md) for all development work in this repository.

Key points:
- Always read `requirements/_index.md` and relevant requirement files before starting any work.
- Follow the Design → Plan → Build phases, stopping for user approval between each phase.
- Document every change as a requirement, no matter how small.
- Pull before editing anything in `requirements/`, commit and push promptly after.
- Follow the API and route conventions defined in [ROUTES.md](ROUTES.md) for all new endpoints and frontend hooks.

## Pre-Commit Validation

See [PRECOMMIT.md](PRECOMMIT.md) for mandatory validation steps before committing any changes. This applies to all top-level package folders that contain changes: `MAP-backend/`, `MAP-frontend/`, `MAP-shared/`, and `MAP-pdf-generator/`.
