# Per-sport field markings defined in sports.json

**Date Added**: 2026-09-28
**Priority**: High
**Status**: Completed

## Problem Statement

Every preset draws football markings on a rectangle, so courts (tennis, pickleball…) and oval grounds (cricket) look wrong, and coverage stats for cricket are clipped to a rectangle instead of the oval.

## Functional Requirements

- Sport definitions (name, standard size, surface shape/colour, markings, 3D fixtures such as goals/posts/nets/hoops/stumps) live in a data file, `sports.json`, next to `index.html`.
- The app loads `sports.json` at startup, builds the sport buttons from it, and renders the selected sport's markings from the data.
- Sports: Football, Futsal, Rugby (union), Cricket, Field hockey, Basketball (FIBA), Netball, Tennis, Volleyball, Badminton, Pickleball.
- Selecting a sport sets the field to its standard size and switches the markings.
- The selected sport is remembered (localStorage) along with the size.
- Surfaces may be `rect` or `ellipse` (cricket). Coverage area / nearest / farthest stats are clipped to the actual surface shape.

## User Experience Requirements

- When length/width are changed away from the standard size, markings rescale using **anchored scaling (option C)**:
  - Marking sizes scale uniformly by `s = min(L/L₀, W/W₀)` so circles stay circular and markings never spill outside the field.
  - Each marking position is anchored per axis to the field centre, the nearest edge, or stretched with the field — e.g. a penalty box stays attached to its goal line; a halfway line always spans the full width.
- The active sport's button is highlighted.
- If `sports.json` cannot be loaded (e.g. page opened via `file://`), a visible message explains that the folder must be served over HTTP, and a plain rectangular field is drawn.

## Technical Requirements

- Coordinates in metres on the standard-size field, origin at centre, `x` along length, `z` along width, `y` up.
- Marking primitives: `outline`, `polyline` (optionally `closed`), `rect` (optionally `fill`), `circle` (optional arc `from`/`to` degrees, optional `y`), `poly3d`. Any may be `dashed` and may `mirror` in `x`, `z` or `xz`.
- `anchor: [ax, az]` with values `centre` (scale about centre), `edge` (keep scaled distance from nearest edge), `stretch` (scale with the field dimension). Default `["centre","centre"]`.
- Heights (`y`) scale by `s`.
- Still a static site; no build step; three.js via CDN as before.

## Acceptance Criteria

- [x] `sports.json` exists and defines all 11 sports; buttons are generated from it.
- [x] Football at 105 × 68 matches the previous markings (plus penalty arcs, corner arcs and front goal posts, which were previously missing).
- [x] Each sport renders its own markings at its standard size.
- [x] Cricket renders an oval ground; coverage stats clip to the oval.
- [x] Changing size away from standard keeps edge-anchored markings attached to their lines and circles circular, with no court markings drawn outside the field (fixtures such as goals and net posts sit just outside, as in reality).
- [x] Selected sport persists across reloads.
- [x] Opening over `file://` shows the HTTP-serving message rather than a blank/broken page.

## Dependencies

Supersedes the `FIELD_PRESETS` array from REQ-002 and the cricket rectangle from REQ-003.

## Implementation Notes

- `index.html` loads `sports.json` with a top-level `await fetch()` in the module script; on failure it uses a built-in plain rectangle (`FALLBACK_SPORT`) and shows the message in the Sport panel.
- `makeMapper()` implements anchored scaling; `markingPaths()` expands primitives into vertices of the form *anchored base point + offset × s*, so circles and 3D fixtures scale uniformly while their positions follow the anchors. `mirror` flips base and offset together.
- Per-point anchors (`anchors: [[ax, az], …]`) were added for lines that span a centre-anchored and an edge-anchored point (badminton and pickleball centre lines).
- Surface fills (e.g. cricket pitch strip) layer via `polygonOffset` rather than y-gaps; the coverage overlay fill now uses `depthTest: false` so it always draws over the ground.
- Coverage clipping generalised from `clipToRect` to `clipToConvex` against `surfacePolygon()` (rect, or a 96-gon for ellipses).
- Presets set exact sizes (e.g. 23.77 × 10.97) through the number inputs, which don't snap to the slider's 0.1 m step.
- Verified in headless Chromium over HTTP: every sport at its standard size, football 60 × 40, tennis 30 × 11, basketball 20 × 15, cricket 120 × 80, reload persistence, and the `file://` message.
- Not in scope: sport-specific default camera positions; rugby in-goal areas; the 5 m / 15 m dashes parallel to the touchlines.
