# Persist the viewing camera in localStorage

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

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

- [x] Orbit/pan/zoom, reload → same view.
- [x] Click a view preset (Top/Side/Iso/From Cam), reload → same view, including From Cam's FOV.
- [x] Old saved state without view fields loads the default view without errors.

## Dependencies

REQ-008 (share link) reuses these fields.

## Implementation Notes

- `state` gained `viewPos`, `viewTarget` and `viewFov` (defaults: the previous hard-coded view), stored in the existing `frustum-viz-state` object; older saves without them get the defaults.
- The orbit camera and `controls.target` are initialised from state. `saveView()` copies the view into state on every OrbitControls `change` (including the damping coast) and after preset clicks, since a FOV-only change such as From Cam doesn't fire `change`.
- Changed from the plan: saves are **throttled** (at most one every 500 ms, always ending with a final save once movement stops), not debounced. `change` fires every frame while the view coasts after release, so a debounce kept postponing the save. The throttle lives in the shared `saveState()` (see REQ-008), and a pending save is written on `pagehide` so a quick reload doesn't lose it.
- Verified in headless Chromium: orbit then reload gives the same view; From Cam then reload keeps FOV 55; legacy saved state loads the default view.
