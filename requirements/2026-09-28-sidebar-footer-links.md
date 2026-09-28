# Sidebar footer links: Share visualisation + Raise a bug

**Date Added**: 2026-09-28
**Priority**: Low
**Status**: In Progress

## Problem Statement

The "Share visualisation" link sits between the controls and the orbit hint, and there is no way for users to report problems.

## Functional Requirements

- Move "Share visualisation" below the "Drag to orbit · Scroll to zoom · Right-drag to pan" hint.
- Add a "Raise a bug" link under "Share visualisation", pointing to https://github.com/nickgrealy/frustrum-visualiser/issues and opening in a new window/tab.

## User Experience Requirements

- Both links use the same style (blue, icon + text, underline on hover); "Raise a bug" has a bug icon in the REQ-005 style.
- Icon to be previewed and approved before implementation.

## Technical Requirements

- `target="_blank"` with `rel="noopener noreferrer"`.
- Share link behaviour from REQ-008 is unchanged (same `#share-link` element, only moved).

## Acceptance Criteria

- [ ] Order at the bottom of the sidebar: orbit hint, Share visualisation, Raise a bug.
- [ ] "Raise a bug" opens the GitHub issues page in a new tab.
- [ ] Share link still matches the address bar.

## Dependencies

Amends the placement decided in REQ-008.

## Implementation Notes

_To be completed after implementation._
