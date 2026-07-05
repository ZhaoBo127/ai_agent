# Skill: Feature PRD Creation

Use this skill for feature, product, UX, workflow, or new-capability tasks before implementation
begins.

## Location and Name

Create the PRD under:

```text
documents/prds/<feature-name>.md
```

Use the feature name from the worktree skill:

```text
documents/prds/feature-<short-slug>-YYYYMMDD.md
```

Example:

```text
documents/prds/feature-loop-engineer-workflows-20260628.md
```

If the repo has an existing PRD/product-doc namespace, follow it. Otherwise use `documents/prds/`.

## Required PRD Process

Before writing the final PRD, inspect and record:

1. Product research: what problem exists, who has it, and why now.
2. Competitor or comparable workflow analysis: how similar products/tools solve it.
3. Production vision: how this fits the product direction, operational model, and customer value.
4. Existing modules and architecture: affected services, UI, APIs, data model, background jobs,
   permissions, billing, and observability.
5. UX/UI principles: existing design system, user flow, accessibility, density, error states, and
   human approval points.
6. User cases and user stories: concrete actor/action/outcome stories.
7. Engineering constraints: what is safe for MVP, what should be deferred, and why.

## Required PRD Sections

```md
# PRD: <feature title>

## Summary
<one paragraph>

## Problem
<user/customer/operator problem>

## Product Research
- Findings:
- Comparable products/workflows:
- Lessons:

## Product Vision Fit
<why this belongs in the product and what outcome matters>

## Users and Use Cases
- As a <user>, I want <capability>, so that <outcome>.

## Current System / Architecture
- Modules touched:
- APIs/data/jobs:
- Auth/permissions:
- Observability/billing/security:

## UX/UI Principles
- Existing patterns to follow:
- Primary flow:
- Empty/error/loading states:
- Accessibility:

## Requirements
- Must:
- Should:
- Could:

## Non-Goals
- ...

## MVP Scope
<smallest useful slice; do not over-design>

## Acceptance Criteria
- ...

## Risks and Open Questions
- ...

## Rollout / Verification
- Tests:
- Manual verification:
- Deploy/rollback notes:
```

Rules:

- Do not over-design. Keep the MVP small enough to implement and verify.
- Do not invent competitor facts; if research is unavailable, say what was checked and what is
  unknown.
- Link or reference the PRD from `.loop/RUNBOOK.md`.
- Implementation should not start until the PRD has acceptance criteria and MVP scope.
