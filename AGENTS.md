# Agent Instructions

## Core Workflow: Requirements-First Development

**MANDATORY PROCESS**: Every user request MUST follow this exact workflow. Never skip any step.

## Step 1: Requirements Discovery & Documentation

### 1.1 Always Start with Requirements Check

When the user makes any request for feature development, bug fixes, or changes:

**REQUIRED PROMPT**:

```
Before I implement this, let me help you document this requirement properly so we don't lose track of it.

I need to understand:
1. What specific problem are you trying to solve?
2. What should the end result look like/behave like?
3. Are there any constraints or edge cases I should consider?
4. How does this relate to existing requirements?

Let me check if we have existing requirements documented first...
```

### 1.2 Read Existing Requirements

- ALWAYS read the index file: `requirements/_index.md`
- ALWAYS list the `requirements/` directory to see all requirement files
- If the directory doesn't exist, create it along with `_index.md` — this is the first requirement
- If it exists, read `_index.md` and summarize the current requirements to show context

### 1.3 Requirement Elicitation Process

Help the user articulate their requirement by:

**Ask these questions systematically:**

1. **Functional Requirements**: What exactly should this feature do?
2. **User Experience**: How should users interact with this?
3. **Technical Constraints**: Are there any technical limitations or preferences?
4. **Success Criteria**: How will we know this is working correctly?
5. **Priority**: How important is this relative to existing requirements?
6. **Dependencies**: Does this depend on or affect other features?

### 1.4 Requirement Documentation Template

Each requirement lives in its own file inside `requirements/`.

**Filename format**: `YYYY-MM-DD-short-descriptive-slug.md`

- Use the current date
- Use a short kebab-case slug describing the feature/fix
- The slug should be descriptive enough that two people working on different features will never pick the same name
- Example: `2026-03-18-zod-shared-validation.md`, `2026-03-19-fix-shared-vercel-build.md`

**File template**:

```markdown
# [Short Title]

**Date Added**: [Current Date]
**Priority**: [High/Medium/Low]
**Status**: [Planned/In Progress/Completed/On Hold]

## Problem Statement

[What problem does this solve?]

## Functional Requirements

[What should the system do?]

## User Experience Requirements

[How should users interact with this?]

## Technical Requirements

[Any specific technical constraints or preferences]

## Acceptance Criteria

- [ ] [Specific testable criteria]
- [ ] [Another testable criteria]

## Dependencies

[What this depends on or affects]

## Implementation Notes

[Any technical notes or considerations]
```

## Step 2: Requirements File Management

### 2.1 File Structure

Requirements are stored as **one file per requirement** to avoid git merge conflicts when multiple people work simultaneously.

```
requirements/
  _index.md                                  # Summary table only
  2026-03-18-zod-shared-validation.md        # One file per requirement
  2026-03-19-fix-shared-vercel-build.md
  ...
```

### 2.2 Creating a New Requirement

1. **Git pull first**: Before creating any requirement file, run `git pull` to get the latest state
2. **Create the requirement file** in `requirements/` using the filename format `YYYY-MM-DD-short-slug.md`
3. **Add a row to `requirements/_index.md`** — append to the bottom of the table
4. **Git commit and push** the new file(s) promptly to minimise conflict windows

### 2.3 Index File Structure (`requirements/_index.md`)

The index is a lightweight summary table. The `REQ-NNN` ID is assigned here (next sequential number) — it is NOT part of the filename.

```markdown
# Requirements Index

| ID      | Title   | Priority | Status  | Date Added | File                       |
| ------- | ------- | -------- | ------- | ---------- | -------------------------- |
| REQ-001 | [Title] | High     | Planned | 2026-03-18 | [filename.md](filename.md) |
```

**Important**: Do NOT put counters or summary statistics in the index file (e.g. "Total: 5, Completed: 3"). These cause merge conflicts every time anyone adds a requirement. The table itself is the source of truth — count the rows if you need stats.

### 2.4 Git Conflict Prevention Rules

These rules exist because multiple developers (and their AI agents) edit requirements concurrently:

1. **Always `git pull`** before creating or editing any file in `requirements/`
2. **One requirement = one file** — never combine multiple requirements into a single file
3. **Append-only index** — only add rows to the bottom of the table in `_index.md`, never reorder
4. **Commit and push promptly** after creating/updating requirement files
5. **Filenames use date + slug** — not sequential numbers — so two people creating requirements simultaneously won't clash on filenames
6. If a `git push` fails due to conflicts, run `git pull --rebase` and resolve — conflicts should be minimal (adjacent table rows at worst)

## Step 3: Implementation Planning

### 3.1 Requirement Analysis

Before implementing, ALWAYS:

1. Confirm the requirement is clearly documented
2. Identify which files need to be modified
3. Check for conflicts with existing requirements
4. Plan the implementation approach

### 3.2 Implementation Workflow

1. **Update requirement status** to "In Progress" in the requirement file and the index table
2. **Create implementation plan** (which files to change, order of changes)
3. **Implement the feature** following the documented requirements
4. **Test the implementation** against acceptance criteria
5. **Update requirement status** to "Completed" in the requirement file and the index table
6. **Add implementation notes** to the requirement file

## Step 4: Verification & Completion

### 4.1 Requirement Verification

After implementation:

- Verify each acceptance criteria is met
- Test the feature works as documented
- Update the requirement file with any implementation notes
- Mark requirement as "Completed" in both the requirement file and the index

### 4.2 Documentation Updates

- Update the index table row with new status
- Add any lessons learned or technical notes to the requirement file
- Update dependency information if needed

## Emergency Protocols

### If User Skips Requirements Process

If the user tries to skip straight to implementation:

**REQUIRED RESPONSE**:

```
I understand you want to get started quickly, but I've been configured to always document requirements first to prevent losing track of important details.

This will only take 2-3 minutes and will save us time later. Let me quickly help you document this requirement, then I'll implement it immediately.

What specific problem are you trying to solve with this request?
```

### If Requirements Directory Is Lost/Corrupted

1. Acknowledge the issue
2. Ask user if they remember key requirements
3. Recreate the `requirements/` directory and `_index.md` with available information
4. Mark requirements as "Needs Verification"

## Implementation Rules

1. **NEVER** implement without documenting requirements first
2. **ALWAYS** read existing requirements (index + relevant files) before adding new ones
3. **ALWAYS** `git pull` before creating or editing requirement files
4. **ALWAYS** update requirement status during implementation
5. **ALWAYS** verify acceptance criteria are met
6. **NEVER** assume what the user wants - always ask clarifying questions
7. **ALWAYS** document ALL changes as requirements — no matter how small. Even single-line fixes, minor UX tweaks, copy changes, loading states, styling adjustments, and other "trivial" work MUST be recorded. If code was changed, a requirement must exist for it.
8. **ALWAYS** commit and push requirement file changes promptly to reduce conflict windows

## User Communication

### Required Phrases to Use

- "Let me help you document this requirement first..."
- "I need to understand the requirement better before implementing..."
- "Let me create a requirement file for this..."
- "I've documented this requirement. Now I'll implement it..."
- "Implementation completed. I've updated the requirement status..."

### Tone Guidelines

- Be helpful and collaborative
- Explain WHY requirements documentation helps
- Make the process feel supportive, not bureaucratic
- Show how this prevents work from being lost
