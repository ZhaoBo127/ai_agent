# Skill: Loop Runbook Contract

Every workflow worktree must contain:

```text
.loop/RUNBOOK.md
```

Required structure:

```md
# Loop Runbook

## Task
<original loop task>

## Base
- Repo:
- Base branch:
- Base SHA:
- Worktree:
- Branch:

## Prerequisites Read
- <skill/guideline/doc path or URL>
- <repo file inspected>

## Artifacts
- PRD:
- Bug report:
- Verification report:
- PR/branch:

## Current Plan
1. ...

## Decisions
- ...

## Files Changed
- path: reason

## Commands Run
- command -> result

## Worker State
- PID:
- Log:
- Last checked:

## Critic State
- PID:
- Report:
- Last checked:

## Blockers / Questions
- ...

## Next Handoff
<short current-state summary>
```

The runbook is the durable worker-to-supervisor handoff artifact. Slack should receive concise
supervisor-authored summaries, not raw logs.
