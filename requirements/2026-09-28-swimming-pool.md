# Add swimming pool

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Planned

## Problem Statement

Swimming pools are commonly filmed venues. Water polo (REQ-016) doesn't show a lane-roped racing pool.

## Functional Requirements

- Add a "Swimming pool" sport: a 50 × 25 m long-course pool with 8 lanes of 2.5 m (plus 1.25 m outer buffers).
- Lane ropes, dark lane stripes on the pool floor with T-marks near each wall, 15 m marks, and backstroke flags 5 m from each end (1.8 m high).

## User Experience Requirements

- Same behaviour as other sports; water-blue surface.

## Technical Requirements

- Existing `sports.json` schema only (rect surface, fills, coloured lines, poly3d flags).

## Acceptance Criteria

- [ ] Pool renders with 8 lanes, lane stripes, 15 m marks and backstroke flags; no page errors.
- [ ] Resizing keeps the end-anchored marks (T-marks, 15 m marks, flags) relative to the walls.

## Dependencies

Uses the REQ-004 schema. Requested alongside REQ-016.

## Implementation Notes

_To be completed after implementation._
