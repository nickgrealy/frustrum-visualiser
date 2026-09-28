# Sport field size presets

**Date Added**: 2026-09-28
**Priority**: Medium
**Status**: Completed

## Problem Statement

Users want to quickly set the field to the standard dimensions of common sports instead of entering length/width by hand.

## Functional Requirements

- A set of preset buttons under Pitch Dimensions; clicking one sets length and width to that sport's standard playing-area size.
- Presets: Football (soccer), Futsal, Rugby, Hockey, Basketball, Netball, Tennis, Volleyball, Badminton, Pickleball.

## User Experience Requirements

- Buttons show the sport name and its dimensions.
- The preset matching the current size is highlighted.
- Presets update the sliders/number inputs and persist like manual edits.

## Technical Requirements

- Sizes are the playing area, excluding run-off; rounded to the 0.1 m step.

## Acceptance Criteria

- [x] Clicking Tennis sets 23.8 × 11 m and highlights Tennis.
- [x] Manual edits that match a preset highlight it.

## Dependencies

Depends on REQ-001 (small minimum sizes). Superseded in part by REQ-004 (presets move to `sports.json`).

## Implementation Notes

Backfilled after implementation (commit `0a68205`). Presets were a `FIELD_PRESETS` array in `index.html`; markings stayed football-only.
