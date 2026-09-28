# Rename "Hurling / Gaelic football" to "Gaelic football"

**Date Added**: 2026-09-28
**Priority**: Low
**Status**: In Progress

## Problem Statement

The button label "Hurling / Gaelic football" (REQ-012) is long; the user prefers "Gaelic football".

## Functional Requirements

- The sport button reads "Gaelic football".

## User Experience Requirements

- The button moves to its new alphabetical position (REQ-011): after Football.

## Technical Requirements

- Change only the `name` in `sports.json`; the id stays `gaelic`, so saved state and shared links (`?sport=gaelic`) are unaffected.
- Pitch and markings unchanged (the pitch is shared by hurling, Gaelic football and camogie).

## Acceptance Criteria

- [ ] Button shows "Gaelic football", sorted after Football.
- [ ] `?sport=gaelic` still loads the pitch.

## Dependencies

Amends the name chosen in REQ-012.

## Implementation Notes

_To be completed after implementation._
