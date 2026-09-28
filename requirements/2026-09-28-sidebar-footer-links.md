# Sidebar footer links: Share visualisation + Raise a bug

**Date Added**: 2026-09-28
**Priority**: Low
**Status**: Completed

## Problem Statement

The "Share visualisation" link sits between the controls and the orbit hint, and there is no way for users to report problems.

## Functional Requirements

- Move "Share visualisation" below the "Drag to orbit · Scroll to zoom · Right-drag to pan" hint.
- Add a "Raise a bug" link under "Share visualisation", pointing to https://github.com/nickgrealy/frustrum-visualiser/issues and opening in a new window/tab.

## User Experience Requirements

- Both links use the same style (blue, icon + text, underline on hover); "Raise a bug" has a bug icon in the REQ-005 style.
- Icon previewed and approved by the user on 2026-09-28.

## Technical Requirements

- `target="_blank"` with `rel="noopener noreferrer"`.
- Share link behaviour from REQ-008 is unchanged (same `#share-link` element, only moved).

## Acceptance Criteria

- [x] Order at the bottom of the sidebar: orbit hint, Share visualisation, Raise a bug.
- [x] "Raise a bug" opens the GitHub issues page in a new tab.
- [x] Share link still matches the address bar.

## Dependencies

Amends the placement decided in REQ-008.

## Implementation Notes

- Both links sit in a `.sidebar-links` flex column (6 px gap) below the orbit hint. The CSS class `.share-link` was renamed to `.sidebar-link` because it now styles both links; the `#share-link` id used by the REQ-008 code is unchanged.
- The bug icon is a new inline SVG (body, head, legs, antennae) in the REQ-005 `.ico` style.
- Verified in headless Chromium: link order below the hint; the bug link's href, `target="_blank"` and `rel="noopener noreferrer"`; clicking it opens a new tab while the original stays put; the share link still matches the address bar after a change; no page errors.
