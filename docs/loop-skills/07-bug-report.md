# Skill: Bug Report Creation

Use this skill for bug, regression, failing-test, incident, or broken-behavior tasks before
implementation begins.

## Location and Name

Create the report under:

```text
documents/bugs/<bug-name>.md
```

Use the same bug name from the worktree skill:

```text
documents/bugs/bug-<short-slug>-YYYYMMDD.md
```

Example:

```text
documents/bugs/bug-storage-billing-pagination-20260628.md
```

If the repo has an existing bug-report namespace, follow it. Otherwise use `documents/bugs/`.

## Required Report Sections

```md
# Bug: <short title>

## Summary
<one paragraph explaining the problem and impact>

## User Description
<quote or summarize the user's original description>

## Evidence
- Screenshots:
- Logs:
- Error messages:
- Links:
- Files inspected:

## Environment
- Repo:
- Branch/worktree:
- Base SHA:
- Date/time:
- Relevant services:

## Reproduction Steps
1. ...
2. ...
3. ...

## Expected Behavior
<what should happen>

## Actual Behavior
<what happens instead>

## Scope / Impact
<who or what is affected>

## Initial Hypotheses
- ...

## Verification Needed
- ...
```

Rules:

- Preserve user screenshots, logs, links, and exact error text when available.
- If evidence is missing, explicitly write `Not provided yet` instead of inventing it.
- Reproduction steps must be concrete enough for a new engineer to attempt.
- Expected and actual behavior must both be present.
- Link or reference the bug report from `.loop/RUNBOOK.md`.
