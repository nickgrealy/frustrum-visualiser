# README "Try it right now!" link

**Date Added**: 2026-09-28
**Priority**: Low
**Status**: In Progress

## Problem Statement

The README doesn't point to the hosted app, so readers can't try it without running it locally.

## Functional Requirements

- Add a "Try it right now!" link after the README description and before the screenshot, pointing to the hosted app (Vercel) with a pre-set swimming-pool view:
  `https://frustrum-visualiser.vercel.app/?sport=swimming-pool&L=50&W=25&cam=24,4.5,-16.5&rot=-29,-45,0&fov=102,67&view=44.36,12.5,9.14&look=-10.35,-5.43,-15.15&vfov=50`

## User Experience Requirements

- Link text exactly "Try it right now!".

## Technical Requirements

- Plain Markdown link; URL used verbatim. All values are within the slider ranges, so the share-link parser (REQ-008) applies them without clamping.

## Acceptance Criteria

- [ ] README shows "Try it right now!" between the description and the image, linking to the URL above.

## Dependencies

REQ-008 (share link parameters), REQ-014 (README), REQ-018 (screenshot position).

## Implementation Notes

_To be completed after implementation._
