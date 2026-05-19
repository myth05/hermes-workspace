# Linear Agent Issue Template

Use this template for work that an AI coding agent can execute safely. The goal is to make each issue self-contained enough that an agent can complete it without wandering, guessing, or refactoring half the house because it found a loose board.

Copy the Markdown below into a Linear issue.

---

```md
## Goal
State the concrete outcome. One issue should produce one reviewable result.

Example: Add a repo-level AGENTS.md that defines the Linear-driven development workflow.

## Context
Provide the minimum background needed to do the work correctly.

Include:
- Why this matters
- Relevant prior decisions
- Related issues/PRs/docs
- Product/user constraints

## Scope
List what the agent is allowed or expected to touch.

- Files/directories likely involved:
  - `path/to/file`
- Systems involved:
  - UI / API / docs / tests / config
- Expected change type:
  - docs / feature / fix / test / refactor

## Out of Scope
Make the boundaries explicit. This is the anti-drift section.

- Do not refactor unrelated code
- Do not change auth/billing/security/deploy config
- Do not add dependencies unless explicitly approved
- Do not rename/move files unless required by acceptance criteria

## Acceptance Criteria
Define what must be true when the task is done.

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

Good criteria are observable. Avoid vague criteria like “make it better.” That phrase owes everyone money.

## Test Plan
List the checks the agent should run.

- [ ] `pnpm test`
- [ ] `pnpm build`
- [ ] `pnpm lint`
- [ ] Targeted check: `<command>`

If checks are not applicable, say why:

- [ ] Not run: documentation-only change

## Agent Rules
- Read this issue before editing.
- Use the Linear-generated branch name when available.
- Work on one issue per branch.
- Do not work on `main`.
- Touch only files required by this issue.
- Open a PR when done.
- Reference this issue in the PR body with `Closes ORD-###` or `Refs ORD-###`.
- Comment on this Linear issue with PR URL, summary, verification, and risks.
- Stop and ask if the work requires credentials, payment, production deploys, security-sensitive changes, or product/taste judgment.

## Links / References
- Linear project: <url>
- Related issue(s): <url>
- Relevant doc(s): <url>
- Related PR(s): <url>

## Completion Comment Format
When the PR is opened, comment with:

PR: <url>

Summary:
- ...

Verification:
- ...

Notes / Risks:
- ...
```

---

## Priority Guidance

Use Linear priority values consistently:

- **Urgent**: active blocker, production issue, or time-sensitive decision
- **High**: important project rail needed soon
- **Medium**: useful next work, not blocking today
- **Low**: cleanup, polish, backlog
- **None**: parking-lot idea, not yet committed

## Recommended Issue Size

An agent-executable issue should usually be completable in one focused PR.

Good issue sizes:
- Add one docs page
- Fix one bug with tests
- Add one small UI state
- Create one integration seam
- Refactor one isolated module

Too large:
- “Build the dashboard”
- “Improve UX”
- “Make agents autonomous”
- “Clean up the repo”

Split large work into a project plus 5-15 high-quality issues. Do not create 90 tickets unless you are trying to summon Jira with a blood ritual.

## Source of Truth

- **Linear**: executable work, status, blockers, acceptance criteria
- **GitHub**: branches, code, PRs, CI, reviews
- **Docs/Obsidian**: durable rationale, strategy, long-form decisions
- **Discord/chat**: approvals, blockers, short human updates
