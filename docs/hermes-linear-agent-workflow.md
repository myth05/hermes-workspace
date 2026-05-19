# Hermes ↔ Linear Agent Workflow

This is the operating workflow for using Linear as Hermes/Lucky's execution board and GitHub as the code-review gate.

The goal is not to create more process. The goal is to let agents do scoped work without drift, while Dave stays in judgment/review mode instead of becoming a task router with better lighting.

## Source of Truth Split

| System | Owns | Does Not Own |
|---|---|---|
| Linear | Executable work, status, acceptance criteria, blockers | Long-form strategy, canon, memory |
| GitHub | Branches, code, PRs, CI, reviews | Task prioritization, product rationale |
| Docs / Obsidian | Durable rationale, strategy, canon, architecture notes | Live issue status |
| Discord / Chat | Approvals, blockers, concise human updates | Raw notification streams, durable project memory |
| Hermes / Lucky | Orchestration, drafting, updates, reviews, context hygiene | Unapproved risky changes, final taste/product calls |

## When Work Belongs in Linear

Use Linear for work that is executable and trackable:

- coding tasks
- docs changes tied to a repo
- integration setup
- bug fixes
- reviewable agent work
- multi-step project rails
- work requiring PRs, acceptance criteria, or status tracking

Do not use Linear for:

- vague ideas not yet committed
- durable lore/canon/strategy
- personal daily todos
- chat transcript storage
- broad “think about this” threads

If it needs to be done, put it in Linear. If it needs to be remembered or reasoned about later, put it in docs/Obsidian.

## Issue Lifecycle

Recommended states:

1. **Backlog** — Captured, not ready or not prioritized
2. **Todo** — Ready to be picked up
3. **In Progress** — Agent or human is actively working
4. **In Review** — PR/open artifact is ready for review
5. **Done** — Merged or explicitly accepted
6. **Canceled / Duplicate** — Closed without action

## Agent Work Loop

Every agent-executable issue follows this loop:

```text
Linear issue → branch → implementation → verification → PR → Linear update → review → merge → Done
```

### 1. Prepare the issue

Before implementation, the issue should include:

- Goal
- Context
- Scope
- Out of Scope
- Acceptance Criteria
- Test Plan
- Links / References

Use [`docs/linear-agent-issue-template.md`](./linear-agent-issue-template.md) for the canonical template.

### 2. Start work

The agent should:

1. Read the Linear issue.
2. Move it to **In Progress** when possible.
3. Use the Linear-generated branch name if available.
4. Start from latest `main` unless told otherwise.
5. Work only on that issue.

### 3. Implement narrowly

The agent should:

- touch only files required by the issue
- avoid unrelated refactors
- avoid dependency additions unless justified
- avoid auth/billing/security/deploy changes without approval
- create follow-up issues for adjacent discoveries instead of silently expanding scope

### 4. Verify

Run the smallest relevant checks.

Common repo checks:

```bash
pnpm test
pnpm build
pnpm lint
git diff --check
```

If checks are skipped, say exactly why.

### 5. Open PR

The PR should reference the Linear issue:

```md
## Linear
Closes ORD-123
```

or:

```md
Refs ORD-123
```

Use `Closes` only when merge should complete the issue.

### 6. Update Linear

When the PR opens:

- move the issue to **In Review**
- comment with PR URL
- summarize what changed
- list verification performed
- note risks/blockers

Example:

```md
PR: https://github.com/myth05/hermes-workspace/pull/2

Summary:
- Added reusable Linear issue template for agent-executable tasks.

Verification:
- Ran `git diff --check`.
- Documentation-only change; no runtime checks needed.

Notes / Risks:
- None.
```

### 7. Review and merge

Dave or a reviewer merges once satisfied. After merge:

- mark the issue **Done** if Linear does not auto-close it
- leave a short final comment if useful
- create follow-up issues only for real next work

## Branch Naming

Prefer Linear-generated branch names. If not available:

```text
<agent-or-user>/<issue-id-lowercase>-short-description
```

Examples:

```text
agentbugsy/ord-7-linear-agent-issue-template
agentbugsy/ord-5-hermes-linear-agent-workflow
```

## PR Standard

Use this PR body shape:

```md
## Summary
- ...

## Linear
Closes ORD-###

## Test Plan
- [x] ...
- [ ] Not run: reason

## Notes / Risks
- ...
```

Keep PRs reviewable. If one PR is trying to solve multiple issues, split it unless the coupling is genuinely unavoidable.

## Dave Notification Policy

Routine progress should stay in Linear/GitHub.

Escalate to Dave in chat only for:

- PRs ready for review
- blockers requiring a decision
- changes involving cost, credentials, security, deployment, or production risk
- taste/product/story judgment calls
- failed checks where human context is needed

Do not send Dave raw status spam. Notification firehoses are just anxiety with timestamps.

## Multi-Agent Rules

When multiple agents are active:

- one issue per branch
- one agent owns one issue at a time unless explicitly paired
- agents must not work on the same files simultaneously without coordination
- reviewer agents should review PRs, not mutate the implementation branch directly unless asked
- large work should be decomposed into 5-15 high-quality issues, not dozens of auto-generated filler tickets

## Risk Gates

Agents must stop and ask before:

- changing auth, billing, secrets, security policy, or production deployment
- spending paid API/media-generation credits
- publishing externally
- deleting user data or irreversible artifacts
- making broad architecture changes outside issue scope
- making final product/taste/story calls

## Good First Pilot Shape

A good pilot task:

- docs or low-risk UI
- small enough for one PR
- has clear acceptance criteria
- has no production deployment
- requires no secrets or payment
- proves Linear ↔ GitHub linking works

The ORD-6 and ORD-7 docs PRs are the initial proof that the loop works.

## Maintenance

If this workflow creates friction, update this document and `AGENTS.md` together.

If agents repeatedly drift, tighten the issue template.

If Dave gets too many notifications, move more routine updates into Linear/GitHub and summarize only decision points.
