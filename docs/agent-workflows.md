# Agent Workflows

This index collects the operating docs for Linear-driven agent work in Hermes Workspace.

Use these docs when turning ambiguous work into scoped Linear issues, GitHub branches, and reviewable PRs.

## Core Docs

1. [Hermes ↔ Linear Agent Workflow](./hermes-linear-agent-workflow.md)
   - Source-of-truth split
   - Issue lifecycle
   - Agent work loop
   - Branch and PR standards
   - Risk gates

2. [Linear Agent Issue Template](./linear-agent-issue-template.md)
   - Copy-pasteable Linear issue template
   - Acceptance criteria format
   - Test plan format
   - Agent rules and completion comment format

3. [Low-Noise Agent Status Reporting Policy](./low-noise-agent-status-reporting.md)
   - When to DM Dave
   - What stays in Linear/GitHub
   - Escalation severity
   - Good and bad update examples

## Standard Loop

```text
Linear issue → branch → focused change → verification → PR → Linear update → review → merge → Done
```

## Pilot Result

The initial pilot used the `myth05/hermes-workspace` repo and proved the Linear/GitHub loop with small documentation PRs:

- ORD-6: Added repo-level `AGENTS.md`
- ORD-7: Added the Linear agent issue template
- ORD-5: Added the Hermes ↔ Linear workflow doc
- ORD-9: Added low-noise status reporting policy

ORD-8 closes the starter pilot by adding this index so the workflow docs are discoverable from one place.

## Operating Rule

If Dave needs to act, decide, or review, summarize in Discord.

If it is routine implementation detail, keep it in Linear/GitHub.

If it is durable rationale, put it in docs/Obsidian.
