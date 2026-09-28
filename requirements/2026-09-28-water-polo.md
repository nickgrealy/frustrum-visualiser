# Add water polo

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Planned

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

- [ ] Pool with 30 × 20 m field of play, coloured side markers and floating goals; no page errors.
- [ ] Resizing keeps markers anchored to the goal lines.

## Dependencies

Uses the REQ-004 schema.

## Design Decisions (user, 2026-09-28)

1. Water polo field of play (not a lane-roped pool).
2. A separate generic swimming pool is added as REQ-017.

## Implementation Notes

_To be completed after implementation._
