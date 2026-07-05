# Skill: Adversarial Verification

Use this skill after the initial workflow artifacts are created and before implementation proceeds.
The supervisor must ask a separate critic Codex run in the same worktree to verify the setup.

## When to Run

Run this after creating:

- the isolated worktree
- the loop branch
- `.loop/RUNBOOK.md`
- `.loop/skills/`
- PRD, if the task is a feature
- bug report, if the task is a bug

## Critic Command

Run from inside the isolated worktree:

```bash
mkdir -p .loop
(codex exec --dangerously-bypass-approvals-and-sandbox -c model_reasoning_effort=xhigh \
  "Before acting, read .loop/skills/08-adversarial-verification.md and .loop/RUNBOOK.md. \
  Verify the loop artifacts created so far. Write your report to .loop/CRITIC.md. \
  Do not modify source code." \
  > .loop/critic.log 2>&1 & echo $! > .loop/critic.pid)
```

## Critic Checklist

The critic must verify:

- Worktree exists and is separate from the supervisor base checkout.
- Worktree was created from latest `origin/main` and records base SHA.
- Branch name follows `loop/<loop-name>`.
- Loop name follows the naming convention:
  - `feature-<short-slug>`
  - `bug-<short-slug>-YYYYMMDD`
  - `review-pr-<number>-YYYYMMDD`
  - `prod-<short-slug>-YYYYMMDD-HHMM`
  - `release-<short-slug>-YYYYMMDD`
- `.loop/RUNBOOK.md` exists and has the required sections.
- `.loop/skills/` contains the relevant shared skills.
- For feature tasks, PRD exists under `documents/prds/`.
- For feature tasks, PRD filename follows `feature-<short-slug>-YYYYMMDD.md`.
- For feature tasks, PRD includes product research, competitor/comparable analysis, product
  vision fit, architecture/modules, UX/UI principles, user stories/use cases, MVP scope,
  non-goals, acceptance criteria, risks, and verification plan.
- For feature tasks, PRD is appropriately scoped and does not over-design.
- For bug tasks, bug report exists under `documents/bugs/`.
- For bug tasks, bug report filename follows `bug-<short-slug>-YYYYMMDD.md`.
- For bug tasks, bug report includes user description, screenshots/log references, logs/error
  evidence if available, reproduction steps, expected behavior, actual behavior, and impact.
- Missing evidence is labeled `Not provided yet`, not fabricated.

## Critic Output

Write `.loop/CRITIC.md` with:

```md
# Adversarial Verification

## Verdict
PASS | CONCERNS

## Findings
- ...

## Required Fixes Before Implementation
- ...
```

The supervisor must read `.loop/CRITIC.md`. If the verdict is `CONCERNS`, fix the artifacts and
rerun or update the critic report before implementation continues.
