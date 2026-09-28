# Add athletics track

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

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

- [x] Track renders as a stadium shape with 8 lanes, infield and finish line.
- [x] Coverage stats clip to the stadium outline.
- [x] Resizing keeps the lanes concentric, with nothing outside the track.

## Dependencies

Uses the REQ-004 schema and the REQ-012 `roundrect` surface.

## Design Decisions (user, 2026-09-28)

- Track only; no field-event areas.

## Implementation Notes

- Committed in the "Add Athletics track (REQ-015)" commit on `main`. `sports.json` entry only, with no renderer changes.
- Geometry: 84.39 m straights; lane lines at radii 36.5 + k × 1.22 m (k = 0…7), each a closed polyline (right and left semicircles, 6° steps); the inner kerb line has the grass infield fill; the outline is the `roundrect` surface with radius 46.26 m (= half-width, so a semicircle). Size 176.91 × 92.52 m.
- Finish line at the end of the home straight (x = +42.195 m) on the −z side, nearest the default camera.
- Points are edge-anchored in x (curves stay attached to each end) and centre-anchored in z. At non-proportional sizes the lanes scale by s = min(L/L₀, W/W₀) and stay concentric; any leftover width shows as extra track surface outside lane 8.
- Verified in headless Chromium: top view at 176.91 × 92.52 and 140 × 80, and a close 3D view of the finish line; no page errors.
