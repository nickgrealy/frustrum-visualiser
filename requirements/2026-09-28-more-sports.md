# Add more sports: ice hockey, American football, Aussie rules, rugby league, hurling / Gaelic football, handball, padel, baseball, table tennis

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

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

- [x] Every new sport renders its markings at its standard size, with no page errors.
- [x] The ice rink has rounded corners; coverage stats clip to the rounded outline.
- [x] Ice hockey lines are visible on the ice surface.
- [x] Baseball renders a fan-shaped field; coverage stats clip to the fan.
- [x] Table tennis shows a raised table (0.76 m) with net on a 14 × 7 m floor.
- [x] "Rugby" is shown as "Rugby union"; `?sport=rugby` links still work.
- [x] Resizing a new sport keeps markings anchored and nothing spills outside the field.

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

One commit per sport, in this order: Rugby union rename (`588d726`), Rugby league (`d4e148a`), Hurling / Gaelic football (`90b8a79`), American football (`ea8bcf9`), Aussie rules (`aea3a42`), Handball (`f8db7dd`), Padel (`574f34c`), Ice hockey (`8154a5a`), Baseball (`906c0fb`), Table tennis (`5563624`).

Renderer additions (each committed with the sport that needed it):
- **Ground-marking clipping** (Aussie rules): non-3D lines are clipped to the surface outline (Cyrus–Beck against the convex outline; boundary points kept). Anchored markings that outgrow a resized field, such as AFL 50 m arcs or the handball 9 m line, stop at the boundary instead of spilling over.
- **`roundrect` surface + `lineColor`** (Ice hockey): the corner radius scales with the markings (`s`) and is capped to fit. `lineColor` is the default for uncoloured lines, and `outline` markings accept `color`.
- **`polygon` surface** (Baseball): a convex point list in standard-size metres, stretched with L/W. Coverage and marking clipping use it unchanged, since both need a convex outline.
- **Ordered fill layers** (Baseball): each fill gets a higher polygonOffset than the previous one, so later fills draw on top (dirt → grass → mound → bases).
- **Raised markings** (Table tennis): `y` on `rect`/`polyline` raises its lines and fill; raised fills sit 5 mm under their lines.

Dimensions used (from the governing bodies' published standards as I know them; not re-checked against live documents in this session, because the sandbox has no web access):
- Ice hockey (NHL): 200 × 85 ft, 28 ft corners; goal lines 11 ft from boards; blue lines 25 ft from centre; circles 15 ft radius; end dots 20 ft from goal line, 22 ft off centre; crease 6 ft; goal 6 × 4 ft.
- American football (NFL): 120 × 53⅓ yd; inbounds lines 70 ft 9 in from sidelines; crossbar 10 ft; uprights 18 ft 6 in apart, 35 ft above crossbar.
- Aussie rules (AFL): no fixed ground size (165 × 135 m typical); 50 m centre square; 3 m / 10 m centre circles; 9 × 6.4 m goal square; 50 m arcs from centre of goal line; posts 6.4 m apart.
- Rugby league: 100 × 68 m in-field; lines every 10 m; posts 5.5 m apart, crossbar 3 m.
- Hurling / Gaelic football (GAA): 145 × 88 m within the 130–145 × 80–90 m range; 13/20/45/65 m lines; 14 × 4.5 m and 19 × 13 m rectangles; 13 m arc; posts 6.5 m apart, crossbar 2.5 m.
- Handball (IHF): 40 × 20 m; 6 m goal area; 9 m free-throw line; 7 m and 4 m marks; goal 3 × 2 m.
- Padel (FIP): 20 × 10 m; service lines 6.95 m from net; net 0.88 m centre / 0.92 m posts; walls simplified (4 m back wall, stepped side glass, 3 m mesh).
- Baseball (MLB): 90 ft bases; rubber 60 ft 6 in from home; 95 ft infield arc; mound 18 ft diameter; 330 ft foul poles and 400 ft to centre (typical, since outfield dimensions vary by park); 60 ft backstop.
- Table tennis (ITTF): table 2.74 × 1.525 × 0.76 m; net 15.25 cm high, extending 15.25 cm past each side; 14 × 7 m playing area.

Verification: a final regression run loaded all 20 sports with no page errors. Each new sport was also screenshotted in headless Chromium at its standard size (top view) and, where relevant, resized and close-up 3D; no page errors. Existing sports re-checked after each renderer change (football, tennis, cricket, basketball).

Simplifications / not included: yard numbers and per-yard hash ticks (hash marks drawn as dashed lines); rugby in-goal areas; ice-hockey boards, trapezoids and hash marks; baseball warning track and per-park outfield shapes; padel wall panels drawn as frames only.
