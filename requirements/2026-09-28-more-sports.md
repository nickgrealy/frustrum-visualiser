# Add more sports: ice hockey, American football, Aussie rules, rugby league, Gaelic games (+ handball, padel)

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Planned

## Problem Statement

Popular regional sports are missing: ice hockey (Canada, US, Northern Europe), American football (US), Aussie rules (Australia), rugby league (Australia, UK) and Gaelic games (Ireland). Handball and padel are popular in Europe.

## Functional Requirements

- Add to `sports.json`, each with standard size, surface, markings and 3D fixtures:
  - **Ice hockey**: rink with rounded corners; red centre and goal lines, blue lines, face-off circles, goal creases, goals.
  - **American football**: 100-yard field plus end zones (109.73 × 48.77 m); goal lines, yard lines every 5 yd, goalposts.
  - **Aussie rules**: oval (default 165 × 135 m); centre square and circles, goal squares, 50 m arcs, goal and behind posts.
  - **Rugby league**: 100 × 68 m; halfway, 10/20/40 m lines, H-posts.
  - **Gaelic games** (hurling / Gaelic football / camogie share one pitch): 145 × 88 m; 13, 20, 45 and 65 m lines, small and large rectangles, 13 m arc, H-posts with net.
  - Optional (pending user decision): **Handball** (40 × 20 m) and **Padel** (20 × 10 m).
- Rename the existing "Rugby" button to "Rugby union". Its id stays `rugby`, so saved state and shared links are unaffected.
- New sports appear in alphabetical order automatically (REQ-011).

## User Experience Requirements

- Same button style and behaviour as existing sports; markings rescale with anchored scaling (REQ-004).
- Ice hockey uses a white ice surface with red/blue markings, since white lines would be invisible on ice.

## Technical Requirements

- New surface shape `roundrect` (rectangle with corner `radius`) for the ice rink: drawing, outline and coverage clipping (it's convex, so the existing convex clip works).
- New optional per-sport `lineColor` (default white), used for ice hockey.
- All sizes fit the current slider limits (≤ 180 × 150 m).
- Dimensions are checked against each governing body's rules when the definitions are written, and sources are noted in the implementation notes.

## Acceptance Criteria

- [ ] Every new sport renders its markings at its standard size, with no page errors.
- [ ] The ice rink has rounded corners; coverage stats clip to the rounded outline.
- [ ] Ice hockey lines are visible on the ice surface.
- [ ] "Rugby" is shown as "Rugby union"; `?sport=rugby` links still work.
- [ ] Resizing a new sport keeps markings anchored and nothing spills outside the field.

## Dependencies

Builds on REQ-004 (`sports.json` schema) and REQ-011 (alphabetical order).

## Open Questions (design)

1. Ice hockey size: NHL (60.96 × 25.91 m, 8.53 m corners) or IIHF/Olympic (60 × 30 m, 8.5 m corners)?
2. Include handball and padel?
3. Gaelic button name: "Gaelic games" or "Hurling / Gaelic football"?

## Implementation Notes

_To be completed after implementation._
