# Persist the viewing camera in localStorage

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Planned

## Problem Statement

The field camera settings survive a reload, but the 3D viewing camera (the orbit view) resets to its default every time, so the user loses the view they set up.

## Functional Requirements

- Save the viewing camera's position, look-at target and lens angle (FOV) to localStorage whenever it changes (orbit, pan, zoom, or a view preset).
- Restore it on page load; fall back to the current default view if nothing is saved.

## User Experience Requirements

- Reloading the page shows exactly the same 3D view.
- Orbiting stays smooth (saving must not cause stutter).

## Technical Requirements

- The viewing camera is an OrbitControls camera: its orientation is fully defined by position + target, so those (not pitch/yaw/roll angles) are stored. Confirmed by user 2026-09-28.
- Saves are debounced; OrbitControls emits `change` every frame while damping.
- Stored alongside the existing `frustum-viz-state` object; older saved state without view fields must still load.

## Acceptance Criteria

- [ ] Orbit/pan/zoom, reload → same view.
- [ ] Click a view preset (Top/Side/Iso/From Cam), reload → same view, including From Cam's FOV.
- [ ] Old saved state without view fields loads the default view without errors.

## Dependencies

REQ-008 (share link) reuses these fields.

## Implementation Notes

_To be completed after implementation._
