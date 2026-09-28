# Cricket preset and wider pitch size range

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

## Problem Statement

Cricket was missing from the presets, and cricket grounds are larger than the old 120 × 90 m maximum.

## Functional Requirements

- Add a Cricket preset at 150 × 135 m (boundary oval bounding box of a typical international ground).
- Raise the maximum pitch length to 180 m and width to 150 m.

## User Experience Requirements

- Cricket appears alongside the other preset buttons.

## Technical Requirements

- None beyond input `max` attributes.

## Acceptance Criteria

- [x] Clicking Cricket sets 150 × 135 m.
- [x] Length accepts up to 180 m; width up to 150 m.

## Dependencies

Extends REQ-002. Oval shape and cricket markings are covered by REQ-004.

## Implementation Notes

Backfilled after implementation (commit `70ed509`).
