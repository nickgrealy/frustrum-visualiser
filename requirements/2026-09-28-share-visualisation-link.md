# "Share visualisation" link

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Planned

## Problem Statement

There is no way to send someone the current setup; they would have to re-enter every value by hand.

## Functional Requirements

- A "Share visualisation" `<a href>` link whose URL points to this page with query parameters for every setting: sport, field length/width, field camera position (x, y, z), orientation (pitch, yaw, roll), H/V FOV, and the viewing camera (position, target, FOV).
- On page load, settings come from query parameters if present, then localStorage, then defaults, field by field.
- The link works wherever the site is hosted (built from the current page's URL).

## User Experience Requirements

- Link placement, click behaviour, and what happens to the address bar after opening a shared link: pending user decision (see design).

## Technical Requirements

- Readable, compact parameter names; numbers rounded to at most 2 decimal places.
- Invalid or out-of-range values are ignored (fall back) or clamped to the control ranges; an unknown sport falls back to the default.
- No server component; still a static site.

## Acceptance Criteria

- [ ] Opening the generated link in a fresh browser (empty localStorage) reproduces the same field, camera, and 3D view.
- [ ] A link with only some parameters fills the rest from localStorage/defaults.
- [ ] Malformed parameters don't break the page.

## Dependencies

Depends on REQ-006 (viewing camera state).

## Implementation Notes

_To be completed after implementation._
