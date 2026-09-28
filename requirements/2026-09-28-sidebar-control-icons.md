# Sidebar section and control icons

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Planned

## Problem Statement

The sidebar is text-only (e.g. "Pitch", "Yaw", "Roll", "Horizontal FOV"), so it isn't immediately obvious what each control does — especially the camera orientation and field-of-view terms.

## Functional Requirements

- Add an icon next to each section title (Camera Position, Camera Orientation, Field of View, Pitch Dimensions, Viewing Camera) and each control label (X, Y, Z, Pitch, Yaw, Roll, Horizontal/Vertical FOV, Length, Width, Sport, Preset).
- Add icons next to the coverage stats (Coverage area, Farthest point, Nearest point).
- Icons illustrate what the control does (e.g. the highlighted axis for X/Y/Z, the rotation direction for pitch/yaw/roll, the opening direction for H/V FOV).

## User Experience Requirements

- Icon set to be reviewed and approved by the user before implementation.
- Icons are small (≈14 px), monochrome, and inherit the label colour so they match the existing dark UI.
- Icons are decorative (`aria-hidden`); the text labels stay unchanged.

## Technical Requirements

- Inline SVG (24×24 viewBox, `stroke="currentColor"`), no icon font or extra network dependency.
- Still a single static `index.html` + `sports.json`; no build step.

## Acceptance Criteria

- [ ] User has approved the icon set.
- [ ] Every section title, control label and stat line listed above has its icon.
- [ ] Icons align vertically with the label text and don't shift the slider layout.
- [ ] No new network requests.

## Dependencies

None. Touches only the sidebar/stat markup and CSS in `index.html`.

## Implementation Notes

_To be completed after implementation._
