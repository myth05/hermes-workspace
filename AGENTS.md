# AGENTS.md

Guidance for AI coding agents working in this repository.

## Operating Model

This repo uses Linear as the execution board and GitHub as the code-review gate. Treat each Linear issue as the unit of work: one issue, one branch, one focused change, one PR.

Do not freewheel. If the requested work is not captured in a Linear issue, create or request an issue before making code changes unless the user explicitly asks for a quick local-only investigation.

## Before Editing

1. Read the assigned Linear issue completely.
2. Confirm the issue contains:
   - Goal
   - Context
   - Scope
   - Out of Scope
   - Acceptance Criteria
   - Test Plan
3. If any of those are missing and the task is ambiguous, ask one concise clarifying question or add a Linear comment documenting the assumption.
4. Check repo state:
   ```bash
   git status --short --branch
   git fetch origin
   ```
5. Start from the latest `main` unless the issue specifies another base:
   ```bash
   git checkout main
   git pull --ff-only origin main
   ```

## Branch Naming

Use the Linear-generated branch name when available. Otherwise use:

```text
<agent-or-user>/<issue-id-lowercase>-short-description
```

Example:

```text
agentbugsy/ord-6-agents-md-template
```

Never work directly on `main`.

## Scope Control

- Touch only files required by the issue.
- Do not refactor unrelated code.
- Do not rename files, move directories, or reformat broad areas unless the issue explicitly calls for it.
- Do not introduce new dependencies without explaining why in the PR body.
- Do not change auth, billing, security-sensitive config, deployment config, or secrets handling without explicit human approval.
- Do not commit secrets, `.env` files, local logs, screenshots, or generated artifacts unless they are intentional tracked docs/assets.

If you discover adjacent problems, do not silently expand scope. Add a Linear comment or create a follow-up issue.

## Implementation Standard

For each issue:

1. Implement the smallest change that satisfies the acceptance criteria.
2. Keep commits focused and conventional:
   ```text
   docs: add Linear agent workflow instructions
   feat: add task status filter
   fix: handle missing workspace config
   test: cover MCP source validation
   ```
3. Prefer existing patterns over new architecture.
4. Preserve user-facing behavior unless the issue asks to change it.
5. Update docs when behavior, setup, or workflows change.

## Verification

Run the smallest relevant checks before opening a PR.

Common checks for this repo:

```bash
pnpm test
pnpm build
pnpm lint
```

If a full check is too expensive or blocked by environment constraints, run the most relevant targeted check and clearly state what was and was not run.

Before committing, also run:

```bash
git diff --check
git status --short
```

For merge/conflict work, explicitly scan touched files for conflict markers:

```bash
git diff --name-only | xargs grep -n '<<<<<<<\|=======\|>>>>>>>' || true
```

## Pull Requests

Open a PR for every code or docs change intended to land.

PR title format:

```text
<type>: concise summary
```

PR body must include:

```md
## Summary
- What changed
- Why it changed

## Linear
Closes ORD-123

## Test Plan
- [x] Command/check run
- [ ] Not run: reason

## Notes / Risks
- Anything reviewers should know
```

Reference the Linear issue using `Closes ORD-123` or `Refs ORD-123` so Linear can attach the PR.

## Linear Updates

When starting work:

- Move the Linear issue to In Progress when possible.
- Leave a short comment if the implementation plan differs from the issue description.

When opening the PR, comment on the Linear issue with:

```md
PR: <url>

Summary:
- ...

Verification:
- ...

Notes:
- ...
```

When blocked, comment with:

```md
Blocked: <specific blocker>
Needed: <exact decision/access/info>
```

Do not mark an issue Done until the PR is merged or the human explicitly accepts the non-PR result.

## Notification Discipline

Keep routine progress in Linear/GitHub. Escalate to Dave only for:

- Blockers requiring a decision
- Risky changes needing approval
- PRs ready for review
- Failed checks that need human context
- Scope changes that affect product/story/security/deployment

No notification firehose. The point is less coordination tax, not prettier noise.

## Source of Truth Split

- Linear: executable work, status, acceptance criteria, blockers
- GitHub: code, branches, PRs, reviews, CI
- Obsidian/docs: durable strategy, rationale, canon, long-form notes
- Discord/chat: decisions, approvals, short status, human interface

If something is a durable decision, update the relevant doc. If something is an executable task, update Linear.
