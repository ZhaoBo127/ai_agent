# Skill: Common Skill Sync

Read this after `01-git-worktree-creation.md`. The loop skills are shared by the supervisor and
any worker or critic Codex session.

After creating a worktree, create a common skill directory:

```bash
mkdir -p .loop/skills
```

The supervisor must make the relevant skills available to workers before starting them. If the
skill files are present on disk, copy them:

```bash
cp <bridge-or-repo-skill-dir>/*.md .loop/skills/
```

If the supervisor only received the skills in its prompt, write the required skill text into
`.loop/skills/<skill-name>.md` before starting a worker or critic. At minimum:

- `01-git-worktree-creation.md`
- `03-supervisor-workflow.md`
- `04-worker-codex-runtime.md`
- `05-runbook-contract.md`
- `06-feature-prd.md` for feature tasks
- `07-bug-report.md` for bug tasks
- `08-adversarial-verification.md`
- `09-teardown.md`

Worker and critic prompts must begin with:

```text
Before acting, read the relevant files in .loop/skills/ and .loop/RUNBOOK.md.
```

Record the synced skill filenames in `.loop/RUNBOOK.md` under `Prerequisites Read`.
