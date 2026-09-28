# Sidebar section and control icons

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

## Problem Statement

The sidebar is text-only (e.g. "Pitch", "Yaw", "Roll", "Horizontal FOV"), so it isn't immediately obvious what each control does — especially the camera orientation and field-of-view terms.

## Functional Requirements

- Add an icon next to each section title (Camera Position, Camera Orientation, Field of View, Pitch Dimensions, Viewing Camera) and each control label (X, Y, Z, Pitch, Yaw, Roll, Horizontal/Vertical FOV, Length, Width, Sport, Preset).
- Add icons next to the coverage stats (Coverage area, Farthest point, Nearest point).
- Replace the ⚽ emoji in the page heading with a neutral camera icon (the app now covers many sports); page `<title>` becomes "Frustum Visualizer".
- No hover tooltips (explicitly out of scope).
- Icons illustrate what the control does (e.g. the highlighted axis for X/Y/Z, the rotation direction for pitch/yaw/roll, the opening direction for H/V FOV).

## User Experience Requirements

- Icon set reviewed and approved by the user on 2026-09-28 with no changes (see preview in Implementation Notes).
- Icons are small (≈14 px), monochrome, and inherit the label colour so they match the existing dark UI.
- Icons are decorative (`aria-hidden`); the text labels stay unchanged.

## Technical Requirements

- Inline SVG (24×24 viewBox, `stroke="currentColor"`), no icon font or extra network dependency.
- Still a single static `index.html` + `sports.json`; no build step.

## Acceptance Criteria

- [x] User has approved the icon set.
- [x] Heading shows a camera icon instead of ⚽.
- [x] Every section title, control label and stat line listed above has its icon.
- [x] Icons align vertically with the label text and don't shift the slider layout.
- [x] No new network requests.

## Dependencies

None. Touches only the sidebar/stat markup and CSS in `index.html`.

## Implementation Notes

Approved design: 20 inline SVG icons (pin, compass, camera+cone, ruler, eye; axis gizmo X/Y/Z; pitch/yaw/roll rotation arrows; H/V FOV wedge with ↔/↕; length/width field with dimension arrow; ball; cube; footprint trapezoid; far/near distance marks).

Build notes:
- 21 inline `<svg class="ico">` elements in `index.html` (20 approved + camera in the heading). Shared `.ico` CSS: 14 px (16 px in the heading), `stroke: currentColor`; `.ico .f` fades the inactive axes on X/Y/Z.
- `.ctrl-label` changed from `justify-content: space-between` to `gap: 6px`; otherwise the label text was pushed to the right edge once an icon was added. Nothing used the space-between layout (the `.val` readout style is unused).
- Section titles and the heading became flex rows. The stats overlay's `<br>` lines became `.stat` flex rows, with icons in the same blue as the stat labels.
- Page `<title>` changed from "Soccer Frustum Visualizer" to "Frustum Visualizer".
- Verified in headless Chromium: all 21 icons render, slider position and width are unchanged from before (x=16, w=207), no page errors, and no requests beyond `index.html`, `sports.json` and three.js.
