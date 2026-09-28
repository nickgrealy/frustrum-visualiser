# "Share visualisation" link

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

## Problem Statement

There is no way to send someone the current setup; they would have to re-enter every value by hand.

## Functional Requirements

- A "Share visualisation" `<a href>` link whose URL points to this page with query parameters for every setting: sport, field length/width, field camera position (x, y, z), orientation (pitch, yaw, roll), H/V FOV, and the viewing camera (position, target, FOV).
- On page load, settings come from query parameters if present, then localStorage, then defaults, field by field.
- The link works wherever the site is hosted (built from the current page's URL).
- Every change (controls, sport, 3D view) updates the address bar in place (`history.replaceState`, no new history entries), so the address bar is always a shareable link to the current setup.
- Opening a link applies its settings and saves them to localStorage.

## User Experience Requirements

- Decided with user 2026-09-28:
  - Plain clickable `<a href>` labelled "Share visualisation" whose `href` is always the current share URL. No clipboard handling; users copy it via right-click or the address bar.
  - Placed at the bottom of the sidebar, below Viewing Camera, with a share icon in the REQ-005 style.
  - The address bar updates live on every change (see Functional Requirements).

## Technical Requirements

- Parameters: `sport`, `L`, `W`, `cam=x,y,z`, `rot=pitch,yaw,roll`, `fov=h,v`, `view=x,y,z`, `look=x,y,z`, `vfov`. Numbers are rounded to at most 2 decimal places.
- Invalid or out-of-range values are ignored (fall back) or clamped to the control ranges; an unknown sport falls back to the default.
- No server component; still a static site.

## Acceptance Criteria

- [x] Opening the generated link in a fresh browser (empty localStorage) reproduces the same field, camera, and 3D view.
- [x] A link with only some parameters fills the rest from localStorage/defaults.
- [x] Malformed parameters don't break the page.
- [x] Changing any control or orbiting updates the address bar without adding browser history entries.
- [x] The link's `href` always matches the address bar.

## Dependencies

Depends on REQ-006 (viewing camera state).

## Implementation Notes

- `PARAMS` maps query params to state keys. `parseNums()` rejects malformed values (wrong count, empty, non-finite); slider-backed values are clamped to their input's `min`/`max`; `vfov` is clamped to 5–120. `sport` is applied only if it exists in `sports.json`.
- Load order per field: defaults → localStorage → URL. At startup `flushState()` writes the merged state back, so an opened link is saved and the address bar and link are populated immediately.
- `saveState()` is throttled (500 ms, with a final save once changes stop). `flushState()` writes localStorage, then calls `history.replaceState` (in try/catch) and sets `#share-link.href = location.href`. The throttle keeps slider drags and orbiting under Safari's limit of about 100 `replaceState` calls per 30 s.
- Commas in vector params are left unescaped for readability.
- Rounding to 2 dp means a reloaded or shared view can differ from the original by ≤ 5 mm, a sub-pixel shift.
- Verified in headless Chromium (18 checks, all passing): default load writes the URL; the link matches the address bar; orbiting and control changes update the URL with no new history entries; a shared link in a fresh browser gives the same URL, the same localStorage and the same frame; a partial link fills the rest from localStorage; garbage params are ignored or clamped; no page errors.
