# Minimum pitch size 13 × 6 m, 0.1 m increments

**Date Added**: 2026-09-25
**Priority**: Medium
**Status**: Completed

## Problem Statement

The pitch size controls only went down to 30 m × 10 m in 1 m steps, which is too coarse and too large to model small courts (e.g. pickleball, badminton).

## Functional Requirements

- Pitch length minimum is 13 m; pitch width minimum is 6 m.
- Both length and width change in 0.1 m increments.

## User Experience Requirements

- Slider and number input both honour the new min/step.
- Values display to one decimal place (e.g. `13.4 m`).

## Technical Requirements

- `min`/`max`/`step` set on both the range and number inputs so browser spinners respect the limits.
- Typed values are clamped to the slider's range.

## Acceptance Criteria

- [x] Length can be set to 13.0 m but not lower.
- [x] Width can be set to 6.0 m but not lower.
- [x] Both values step by 0.1 m.

## Dependencies

Enables REQ-002 (small-court presets).

## Implementation Notes

Backfilled after implementation (commit `b85ed2d`). Changes in `index.html` input attributes and `wireControl('fieldL'|'fieldW', …, fmtM)`.
