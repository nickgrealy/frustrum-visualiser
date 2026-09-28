# Add athletics track

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: In Progress

## Problem Statement

Athletics stadiums are among the most commonly filmed venues, but there's no athletics track preset.

## Functional Requirements

- Add an "Athletics track" sport: a standard 400 m track (World Athletics layout: 84.39 m straights, 36.5 m inner radius, 8 lanes of 1.22 m).
- Default size is the track's outer bounding box, ~176.9 × 92.5 m (within the 180 × 150 m limit).
- Stadium-shaped (straights + semicircles) surface in track red, with a grass infield, lane lines and the finish line.

## User Experience Requirements

- Same behaviour as other sports; markings rescale with anchored scaling, and the lanes keep their shape when resized.

## Technical Requirements

- Stadium shape via the existing `roundrect` surface with radius ≥ half the width (capped to a semicircle).
- Lane lines and the infield generated as closed polylines, edge-anchored so the curves stay attached to each end.

## Acceptance Criteria

- [ ] Track renders as a stadium shape with 8 lanes, infield and finish line.
- [ ] Coverage stats clip to the stadium outline.
- [ ] Resizing keeps the lanes concentric, with nothing outside the track.

## Dependencies

Uses the REQ-004 schema and the REQ-012 `roundrect` surface.

## Design Decisions (user, 2026-09-28)

- Track only; no field-event areas.

## Implementation Notes

_To be completed after implementation._
