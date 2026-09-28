# Add water polo

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

## Problem Statement

There's no aquatic venue preset; water polo was requested.

## Functional Requirements

- Add a "Water polo" sport: a 33 × 25 m pool containing the 30 × 20 m field of play (men's).
- Field of play outlined by floating perimeter ropes; no lane ropes.
- Side markers along both sides: goal lines (white), 2 m (red), 5 m (yellow), halfway (white).
- Floating goals: 3 m wide, 0.9 m above the water.

## User Experience Requirements

- Same behaviour as other sports; water-blue surface.

## Technical Requirements

- Uses the existing `sports.json` schema (rect surface, coloured lines, poly3d goals).

## Acceptance Criteria

- [x] Pool with 30 × 20 m field of play, coloured side markers and floating goals; no page errors.
- [x] Resizing keeps markers anchored to the goal lines.

## Dependencies

Uses the REQ-004 schema.

## Design Decisions (user, 2026-09-28)

1. Water polo field of play (not a lane-roped pool).
2. A separate generic swimming pool is added as REQ-017.

## Implementation Notes

- Committed in the "Add Water polo (REQ-016)" commit on `main`. `sports.json` entry only, with no renderer changes.
- Pool 33 × 25 m (1.5 m behind each goal line, 2.5 m beside the field of play); field of play 30 × 20 m drawn as a dashed rope outline (edge-anchored).
- Side markers are 1.2 m ticks across the side ropes at the goal lines (white), 2 m (red `#e03131`), 5 m (yellow `#f2c94c`) and halfway (white), edge-anchored so they stay measured from the goal lines.
- Goals: 3 m wide, 0.9 m above the water, 0.3 m deep net frame.
- Verified in headless Chromium: top view at 33 × 25 and 25 × 20, and a close 3D view of goals and markers; no page errors.
