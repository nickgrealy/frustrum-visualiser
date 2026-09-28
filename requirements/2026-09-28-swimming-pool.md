# Add swimming pool

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

## Problem Statement

Swimming pools are commonly filmed venues. Water polo (REQ-016) doesn't show a lane-roped racing pool.

## Functional Requirements

- Add a "Swimming pool" sport: a 50 × 25 m long-course pool with 8 racing lanes of 2.5 m plus a 2.5 m outer lane on each side (10 × 2.5 m = 25 m, as in Olympic pools).
- Lane ropes, dark lane stripes on the pool floor with T-marks near each wall, 15 m marks, and backstroke flags 5 m from each end (1.8 m high).

## User Experience Requirements

- Same behaviour as other sports; water-blue surface.

## Technical Requirements

- Existing `sports.json` schema only (rect surface, fills, coloured lines, poly3d flags).

## Acceptance Criteria

- [x] Pool renders with 8 lanes, lane stripes, 15 m marks and backstroke flags; no page errors.
- [x] Resizing keeps the end-anchored marks (T-marks, 15 m marks, flags) relative to the walls.

## Dependencies

Uses the REQ-004 schema. Requested alongside REQ-016.

## Implementation Notes

- Committed in the "Add Swimming pool (REQ-017)" commit on `main`. `sports.json` entry only, with no renderer changes.
- Layout corrected from the first draft ("1.25 m buffers" didn't sum to 25 m): 10 × 2.5 m lanes, 8 racing lanes plus an empty outer lane each side.
- 9 dashed lane ropes (stretch-anchored so lanes divide the width evenly); 0.25 m dark lane stripes for the 8 racing lanes ending 2 m from each wall, with 1 m T-bars; red dashed 15 m lines; yellow backstroke-flag lines 1.8 m high, 5 m from each wall.
- Verified in headless Chromium: top view at 50 × 25 and 25 × 15, and a close 3D view; no page errors.
