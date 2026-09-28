# README screenshot (swimming pool)

**Date Added**: 2026-09-28
**Priority**: Low
**Status**: Completed

## Problem Statement

The README (REQ-014) is text-only; a screenshot shows at a glance what the tool does.

## Functional Requirements

- Commit the swimming-pool close-up screenshot taken during REQ-017 (1100 × 900 PNG, ~60 KB) to the repo.
- Show it in `README.md` directly below the introduction paragraph.

## User Experience Requirements

- Image has descriptive alt text and renders on GitHub.

## Technical Requirements

- Stored as `docs/images/swimming-pool.png`, referenced with a relative path.

## Acceptance Criteria

- [x] Image file committed at the path above.
- [x] README shows the image below the intro (relative link resolves).

## Dependencies

REQ-014 (README), REQ-017 (screenshot source).

## Implementation Notes

- `docs/images/swimming-pool.png` (1100 × 900, ~60 KB) is the REQ-017 close-up: lanes, T-bars, backstroke flags and the coverage stats overlay.
- README embeds it below the intro paragraph as `![Swimming pool with camera coverage in the 3D view](docs/images/swimming-pool.png)`; the relative path resolves from the repo root.
