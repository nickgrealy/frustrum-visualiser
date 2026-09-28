# Show sports alphabetically

**Date Added**: 2026-09-28
**Priority**: Low
**Status**: Planned

## Problem Statement

The sport buttons appear in `sports.json` order (Football, Futsal, Rugby, Cricket…), which makes a given sport harder to find as the list grows.

## Functional Requirements

- Sport buttons are shown in alphabetical order by display name: Badminton, Basketball, Cricket, Football, Futsal, Hockey, Netball, Pickleball, Rugby, Tennis, Volleyball.
- Sports added to `sports.json` later appear in the right place automatically.

## User Experience Requirements

- No other change to the buttons (same style, active highlight, sizes).

## Technical Requirements

- Sort by `name` in code, case-insensitively (`localeCompare`), when building the buttons. `sports.json` order stays as-is and doesn't need to be kept sorted.
- The default/fallback sport for unknown ids stays the first entry in `sports.json` (Football), so existing behaviour and saved/shared links are unaffected.

## Acceptance Criteria

- [ ] Buttons render in the alphabetical order above.
- [ ] A fresh load still defaults to Football.
- [ ] The active sport is still highlighted, and clicking a button still selects it.

## Dependencies

Builds on REQ-004 (buttons generated from `sports.json`).

## Implementation Notes

_To be completed after implementation._
