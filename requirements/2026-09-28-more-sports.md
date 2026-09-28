# Add more sports: ice hockey, American football, Aussie rules, rugby league, hurling / Gaelic football, handball, padel, baseball, table tennis

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: In Progress

## Problem Statement

Popular regional sports are missing: ice hockey (Canada, US, Northern Europe), American football (US), Aussie rules (Australia), rugby league (Australia, UK) and Gaelic games (Ireland). Handball and padel are popular in Europe. Baseball (US, Japan, Latin America) and table tennis are among the most-played sports worldwide.

## Functional Requirements

- Add to `sports.json`, each with standard size, surface, markings and 3D fixtures:
  - **Ice hockey** (NHL, 60.96 × 25.91 m, 8.53 m corner radius): rink with rounded corners; red centre and goal lines, blue lines, face-off circles, goal creases, goals.
  - **American football**: 100-yard field plus end zones (109.73 × 48.77 m); goal lines, yard lines every 5 yd, goalposts.
  - **Aussie rules**: oval (default 165 × 135 m); centre square and circles, goal squares, 50 m arcs, goal and behind posts.
  - **Rugby league**: 100 × 68 m; halfway, 10/20/40 m lines, H-posts.
  - **Hurling / Gaelic football** (button name; one pitch shared by hurling, Gaelic football and camogie): 145 × 88 m; 13, 20, 45 and 65 m lines, small and large rectangles, 13 m arc, H-posts with net.
  - **Handball** (40 × 20 m): 6 m goal area, dashed 9 m free-throw line, 7 m mark, 4 m goalkeeper line, goals.
  - **Padel** (20 × 10 m): service lines, centre service line, net, simplified glass/mesh wall frames.
  - **Baseball** (MLB): fan-shaped field, foul lines to ~100 m poles, ~122 m to centre field, ~18 m backstop behind home. Infield dirt, grass diamond, bases, pitcher's mound, batter's area. Proposed default size: 140 × 141 m (bounding box of the fan).
  - **Table tennis**: the "field" is the ITTF playing area (14 × 7 m floor), with the 2.74 × 1.525 m table drawn as a raised 3D object at 0.76 m, plus its net. The table alone is below the 13 × 6 m minimum field size, and the camera needs to cover the players' area anyway.
- Rename the existing "Rugby" button to "Rugby union". Its id stays `rugby`, so saved state and shared links are unaffected.
- New sports appear in alphabetical order automatically (REQ-011).

## User Experience Requirements

- Same button style and behaviour as existing sports; markings rescale with anchored scaling (REQ-004).
- Ice hockey uses a white ice surface with red/blue markings, since white lines would be invisible on ice.

## Technical Requirements

- New surface shape `roundrect` (rectangle with corner `radius`) for the ice rink: drawing, outline and coverage clipping (it's convex, so the existing convex clip works).
- New optional per-sport `lineColor` (default white), used for ice hockey.
- New surface shape `polygon` (convex list of points, stretched with the field) for baseball's fan shape; coverage clipping uses the same convex clip.
- Fills on any closed marking (circles, closed polylines), not just rects, and later fills layer above earlier ones (baseball dirt/grass).
- Raised fills (`y` on a filled marking) for the table-tennis table top.
- All sizes fit the current slider limits (≤ 180 × 150 m).
- Dimensions are checked against each governing body's rules when the definitions are written, and sources are noted in the implementation notes.

## Acceptance Criteria

- [ ] Every new sport renders its markings at its standard size, with no page errors.
- [ ] The ice rink has rounded corners; coverage stats clip to the rounded outline.
- [ ] Ice hockey lines are visible on the ice surface.
- [ ] Baseball renders a fan-shaped field; coverage stats clip to the fan.
- [ ] Table tennis shows a raised table (0.76 m) with net on a 14 × 7 m floor.
- [ ] "Rugby" is shown as "Rugby union"; `?sport=rugby` links still work.
- [ ] Resizing a new sport keeps markings anchored and nothing spills outside the field.

## Dependencies

Builds on REQ-004 (`sports.json` schema) and REQ-011 (alphabetical order).

## Design Decisions (user, 2026-09-28)

1. Ice hockey: NHL size.
2. Include handball and padel: yes.
3. Gaelic button name: "Hurling / Gaelic football".
4. Also add baseball and table tennis (raised table).
5. Work through the sports one at a time, one commit per sport.

## Open Questions (design)

6. Table tennis: field = 14 × 7 m playing area with a raised table (see above)?
7. Baseball: MLB-style fan field, 140 × 141 m default, coverage clipped to the fan?

## Implementation Notes

_To be completed after implementation._
