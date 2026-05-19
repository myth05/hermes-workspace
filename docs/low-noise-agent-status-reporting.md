# Low-Noise Agent Status Reporting Policy

This policy defines where agent work updates should go so Dave sees decisions and review points, not a confetti cannon of routine status events.

The rule is simple: keep machine chatter in machine systems. Escalate to Dave only when human judgment is useful.

## Channels and Destinations

| Destination | Use For | Avoid |
|---|---|---|
| Linear issue comments | Work logs, blockers, PR links, verification notes | Long essays, vague status, duplicate GitHub events |
| GitHub PRs | Code review, CI/check status, implementation details | Project planning, unrelated follow-ups |
| Discord DM | Decisions, blockers, review-ready summaries | Routine status, every issue transition, every commit |
| Discord `#work-log` | Compact daily/session work summaries if needed | Raw notification firehose |
| Discord `#briefings` | Higher-level periodic synthesis | Single-task updates |
| Docs / Obsidian | Durable process, rationale, strategy | Live task status |

## Default Reporting Rule

For routine agent work:

```text
Linear/GitHub first. Discord only if Dave needs to act.
```

Examples:

- Branch created → no DM
- Commit pushed → no DM
- PR opened → DM only if ready for Dave review
- Checks passed → Linear/GitHub only unless Dave is waiting
- Checks failed → DM only if human context/approval is needed
- Issue moved In Progress → no DM
- Issue moved Done → no DM unless it completes a meaningful milestone

## DM Dave When

Send a concise Discord DM when:

1. **Review is needed**
   - A PR is ready for Dave to inspect or merge.

2. **A decision is needed**
   - Product/taste/story judgment
   - Architecture tradeoff
   - Scope change
   - Priority conflict

3. **Approval is required**
   - Credentials
   - Payment or API spend
   - Production deployment
   - Security-sensitive change
   - Data deletion or irreversible action

4. **The agent is blocked**
   - Missing access
   - Ambiguous requirement
   - Failing check that needs human context
   - External dependency unavailable

5. **A meaningful milestone completed**
   - Project rail established
   - Pilot loop proven
   - Release-ready package created

## Do Not DM Dave For

Do not DM for:

- every Linear status transition
- every GitHub commit
- every PR sync event
- “still working” updates without new information
- logs copied from CI without interpretation
- agent self-narration
- “I will now...” messages when the action can just be done

If the update does not change Dave's next action, keep it out of DM.

## DM Format

Use this compact shape:

```md
Ready for review: <thing>

What changed:
- ...

Verification:
- ...

Decision needed:
- Merge / approve / choose A vs B / unblock X

Link: <url>
```

For blockers:

```md
Blocked: <specific blocker>

Tried:
- ...

Need from you:
- ...

Link: <issue/pr/doc>
```

## Linear Comment Format

Routine implementation updates belong on the Linear issue:

```md
PR: <url>

Summary:
- ...

Verification:
- ...

Notes / Risks:
- ...
```

For blockers:

```md
Blocked: <specific blocker>

Tried:
- ...

Needed:
- ...
```

## GitHub PR Comment Format

Use PR comments for implementation/review-specific details:

```md
Local verification:
- ...

CI status:
- ...

Notes:
- ...
```

Do not duplicate every Linear comment into GitHub or every GitHub comment into Linear. Cross-link the important artifact and summarize once.

## Summary Cadence

For a short session with one or two PRs, summarize only when Dave needs review.

For longer agent sessions, send one compact end-of-session summary:

```md
Session result:
- Done: ...
- Ready for review: ...
- Blocked: ...
- Next: ...
```

For recurring or autonomous work, prefer a daily/weekly synthesized briefing over raw events.

## Escalation Severity

| Severity | Meaning | Destination |
|---|---|---|
| P0 | Security/prod/data/cost risk needing immediate human approval | DM Dave immediately |
| P1 | Blocking progress or review needed | DM Dave |
| P2 | Normal progress, PR opened, checks complete | Linear/GitHub; DM only if review requested |
| P3 | Routine bookkeeping | Linear/GitHub only |

## Examples

### Good DM

```md
Ready for review: ORD-9 reporting policy

What changed:
- Added low-noise reporting rules for Linear/GitHub/Discord.
- Defined when to DM vs keep updates in Linear.

Verification:
- `git diff --check`

Decision needed:
- Merge PR #4 if this policy matches how you want updates handled.

Link: https://github.com/myth05/hermes-workspace/pull/4
```

### Bad DM

```text
I created a branch.
I added a file.
I committed the file.
I pushed the branch.
I opened a PR.
```

That belongs in logs, not Dave's attention field.

## Review Rule

Before sending any update to Dave, ask:

```text
Does Dave need to act, decide, or know this now?
```

If no, put it in Linear/GitHub and keep moving.
