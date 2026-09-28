# Field camera centreline in a strong colour

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Planned

## Problem Statement

The field camera's centreline (the three.js CameraHelper "target" line from the lens to the centre of the far plane) is white, the same as the field markings, so it is hard to tell apart.

## Functional Requirements

- Draw the centreline in red (`#ff3b30`, chosen by user 2026-09-28): it stands out from white markings and every sport's surface colour (green, blue, orange, wood), and matches the helper's existing red cone lines.

## User Experience Requirements

- Clearly visible in both the main view and the Camera POV inset.

## Technical Requirements

- Use `CameraHelper.setColors()`; the helper is rebuilt on every camera update, so apply the colour each time.
- Other helper colours are unchanged.

## Acceptance Criteria

- [ ] The centreline is drawn in red on every sport's surface.
- [ ] It stays red after moving the camera.

## Dependencies

None.

## Implementation Notes

_To be completed after implementation._
