# Rename "Hurling / Gaelic football" to "Gaelic football"

**Date Added**: 2026-09-28
**Priority**: Low
**Status**: Completed

## Problem Statement

The button label "Hurling / Gaelic football" (REQ-012) is long; the user prefers "Gaelic football".

## Functional Requirements

- The sport button reads "Gaelic football".

## User Experience Requirements

- The button moves to its new alphabetical position (REQ-011): between Futsal and Handball.

## Technical Requirements

- Change only the `name` in `sports.json`; the id stays `gaelic`, so saved state and shared links (`?sport=gaelic`) are unaffected.
- Pitch and markings unchanged (the pitch is shared by hurling, Gaelic football and camogie).

## Acceptance Criteria

- [x] Button shows "Gaelic football", sorted between Futsal and Handball.
- [x] `?sport=gaelic` still loads the pitch.

## Dependencies

Amends the name chosen in REQ-012.

## Implementation Notes

- One-line change to `name` in `sports.json`; id `gaelic` unchanged.
- Verified in headless Chromium: the button reads "Gaelic football" between Futsal and Handball; `?sport=gaelic` selects and highlights it (the URL keeps `sport=gaelic`); no page errors. A link with only `sport=` takes its size from saved state or the defaults, as each field falls back independently (REQ-008).
