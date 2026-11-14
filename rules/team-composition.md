# Team composition

Shared rules for every engineering-team run. The entry point is [`../SKILL.md`](../SKILL.md).

**Roles define responsibility. Levels define depth.** A role is what an agent is responsible for (systems architect, QA, reviewer). A level is how deep that agent goes (senior, mid-level, junior). Distinct roles stop the team converging on one view; mixed levels add diversity without forcing seniority.

## Capability levels

| Level | Model | Purpose |
|---|---|---|
| Senior | Sonnet, or Opus for high-risk decisions | Deep reasoning, architecture, security, long-term trade-offs |
| Mid-level | Sonnet | Practical planning, implementation, assurance, review |
| Junior | Haiku | Assumptions, simple gaps, direct challenge, broad coverage |

Choose the mix from:

- The risk and complexity of the work.
- The importance of the role to the brief.
- The need for architectural depth versus practical delivery input.
- The need for simple challenge and assumption-checking (the case for a junior).

Use Opus only for senior agents on high-risk decisions.

## Specialist panels

For each selected specialist role, use one of:

| Agents | Allowed mix |
|---:|---|
| 1 | Senior or mid-level |
| 2 | Any mix of senior and mid-level |
| 3 | Two senior or mid-level agents in any mix, plus one junior as the third member; or three senior or mid-level agents |

A junior is only ever the third member of a panel, never one of the first two. Add more senior or mid-level agents only when more depth is needed. **Never more than one junior per specialist role.** Do not force every role to have both a senior and a mid-level agent: one mid-level agent is often enough.

| Senior | Mid-level | Junior | Valid? |
|---:|---:|---:|---|
| 1 | 0 | 0 | Yes |
| 0 | 1 | 0 | Yes |
| 1 | 1 | 0 | Yes |
| 2 | 0 | 0 | Yes |
| 1 | 1 | 1 | Yes |
| 0 | 2 | 1 | Yes |
| 0 | 0 | 1 | No: a junior never works alone |
| 0 | 1 | 1 | No: a junior is only the third member |
| 0 | 0 | 2 | No: two juniors |
| 0 | 1 | 2 | No: two juniors |

## Always-present roles

| Role | When | Composition |
|---|---|---|
| QA | Always | At most two: one senior and one mid-level. **No junior QA.** |
| Developer representative | Always | One mid-level; senior for high-risk, architectural or security-sensitive work. |
| Reviewer | Medium and large teams | One mid-level; senior for high-risk, architectural or security-sensitive work. Does not debate: see Reviewer checks. |

QA is a role, not a level. Use more than one developer representative or reviewer only when the brief genuinely needs separate perspectives. Role files hold the details: [`../roles/qa.md`](../roles/qa.md), [`../roles/developer-representative.md`](../roles/developer-representative.md), [`../roles/reviewer.md`](../roles/reviewer.md).

## Team sizing

**The lead is not counted in these sizes.** It is the main session, not a spawned agent, but it is a full member of the team and takes part in the debate. The reviewer is counted but does not debate, so a medium team has 4 to 6 debaters and a large team 8 to 10.

| Preset | Use for | Total | Specialist agents | QA | Developer rep | Reviewer |
|---|---|---:|---:|---:|---:|---:|
| Lite | Small, low-risk changes with one real design choice | 3 | 1 | 1 | 1 | 0 |
| Medium | Normal feature work | 5 to 7 | 2 to 4 | 1 or 2 | 1 | 1 |
| Large | Complex, high-risk or multi-area work | 9 to 11 | 5 to 7 | 2 | 1 | 1 |

Pick the smallest preset that covers the brief. Work with no real design choice (a one-file fix, a clear bug, a small edit) gets no team at all. Keep the total odd: if a count lands on an even number, drop the least material agent, or add a junior challenger to a role that has room.

## Examples

**Simple UI change** — Medium, 5 agents. No senior is needed when the work is simple.

| Role | Level | Count |
|---|---|---:|
| UX planner | Mid-level | 1 |
| Frontend planner | Mid-level | 1 |
| Developer representative | Mid-level | 1 |
| QA | Mid-level | 1 |
| Reviewer | Mid-level | 1 |

**Backend API feature** (new endpoint with business rules and data changes) — Medium, 7 agents.

| Role | Level | Count |
|---|---|---:|
| Product planner | Senior | 1 |
| Systems architect | Mid-level | 1 |
| Backend planner | Senior | 1 |
| Data planner | Mid-level | 1 |
| Developer representative | Mid-level | 1 |
| QA | Senior | 1 |
| Reviewer | Mid-level | 1 |

**Complex backend migration** — Large, 9 agents, with strong architectural and data depth.

| Role | Level | Count |
|---|---|---:|
| Systems architect | Senior (Opus) | 2 |
| Backend planner | Senior, mid-level | 2 |
| Data planner | Senior (Opus) | 1 |
| Developer representative | Senior | 1 |
| QA | Senior, mid-level | 2 |
| Reviewer | Senior | 1 |

**Payments or sensitive data** (payments, personal data, permissions, regulated workflows) — Large, 9 agents.

| Role | Level | Count |
|---|---|---:|
| Product planner | Senior | 1 |
| Systems architect | Senior | 1 |
| Backend planner | Mid-level | 1 |
| Data planner | Senior (Opus) | 1 |
| Security planner | Senior (Opus) | 1 |
| Developer representative | Senior | 1 |
| QA | Senior, mid-level | 2 |
| Reviewer | Senior | 1 |

## Role selection

Select only the roles that are material to the brief.

| If the brief involves… | Select |
|---|---|
| User-facing feature | Product, UX, frontend, QA |
| Business logic or API | Product, systems architect, backend, QA |
| Database or reporting | Data planner, systems architect, QA |
| Third-party integration | Integration planner, backend, QA |
| Authentication or sensitive data | Security planner, systems architect, QA |
| Deployment or infrastructure | DevOps planner, systems architect, QA |
| Performance-sensitive work | Performance planner, systems architect, QA |
| Public-facing documentation | Documentation planner, product planner, QA |
| Success measurement | Analytics planner, product planner, QA |

When several rows match, merge them and drop duplicates. If the merged list is too big for the preset, keep the roles with the highest risk to the brief.

## Selection order

1. Read the approved brief and the repository findings.
2. Select only the specialist roles the brief needs.
3. Fill each one with a mixed-level panel, at most one junior each.
4. Add the developer representative.
5. Add QA: one or two agents, never junior.
6. Add the reviewer for medium and large teams.
7. Check the total fits a preset and is odd.

## Token estimate

Rough cost per agent per round, input and output together, with terse notes:

| Model | Per round |
|---|---:|
| Haiku | ~5k |
| Sonnet | ~15k |
| Opus | ~25k |

Estimate = (agents × per-round cost × rounds expected) + the lead's overview pass (~5k) + code exploration in round 1 (~10–30k per debater, less for juniors, who only check what they challenge) + the lead's own round 1 position (~15k) + QA ticket pass (~5–10k per QA agent) + lead synthesis (~15k) + ticket drafting (~2–3k per ticket). Medium and large teams add the reviewer: ~15k for the draft check, ~15–20k for the ticket check and ~15–25k for the code check. Continuing agents with SendMessage instead of spawning new ones keeps round 2 cheaper. Round 2 only includes agents in a material disagreement, so count them separately. Give the user one total and the per-agent breakdown. These figures are first guesses: correct them after real runs.

## Debate

**Two rounds at most.** The lead is a member of the team: it explores the code, writes its own round 1 position and takes part in round 2. Round 1 runs every debater in parallel; the four-at-once limit applies to round 2, where agents respond to each other. The reviewer does not debate. Every agent's output goes back to the lead in full. Nothing is summarised away between an agent and the lead.

### Terse notes

Agents write for the lead, not for people, so they use short notes instead of prose: fragments, no filler, no restating the brief. Terse means fewer words, never fewer facts:

- Every field in the format below is present, every time. Nothing to say → `none`. Don't know → `unknown: <what is missing>`.
- Every risk, assumption, objection and question is its own line. Never merge two into one.
- File paths, function names, numbers, versions and error text are copied exactly.
- Each point gets an ID made of the role, the level letter (`S`, `M` or `J`) and a number, such as `SEC-S1`, `SEC-M1` or `QA-S3`, so two agents in the same role never clash. The lead uses `LEAD-1`, `LEAD-2`; the reviewer uses `REV-1`, `REV-2`.

Tickets and anything shown to the user are written in plain sentences, not notes.

### Exploring the code

The team reads the code, not just the lead. In round 1, every debater (the lead included) explores the parts of the codebase its role covers:

1. Query Graphify first, if installed: `graphify query`, `graphify path`, `graphify explain`. The lead's overview and [`../companions/graphify.md`](../companions/graphify.md) say which areas each role covers.
2. Then open the files the graph (or a search) points to. Read only what the argument needs.
3. **Read-only.** Nobody changes code during the debate. Building starts after confirmation 2.
4. **Evidence for every claim.** Any statement about existing code cites where it comes from, such as `src/auth.ts:42`. Anything not checked is marked `unchecked`, so the reviewer can see which claims have nothing behind them.

### Round 1: independent positions

Each debater works alone, from the brief, the lead's overview, its own exploration of the code, its role file and the Ponytail rules. **The lead writes its own position before reading anyone else's**, so it doesn't anchor on theirs. Each returns:

```
ROLE / LEVEL:
REC:          recommendation, and which Ponytail step it stops at
WHY:          reasoning
RISKS:        one per line, with ID
ASSUMES:      one per line, with ID
EVIDENCE:     path:line for each claim about existing code; `unchecked` where not checked
CHANGE-MIND:  what would change the recommendation
QUESTIONS:    anything it needs answered, one per line, with ID
TICKETS:      proposed tickets for its area: task, files or component, done means
```

### QA ticket pass

After round 1, the lead sends every agent's proposed tickets to the QA agents (continued with SendMessage). QA returns acceptance criteria and tests for each proposed ticket, with IDs. This is not a debate round: QA adds to the tickets, it does not argue positions. Any disagreement QA raises goes into round 2.

### Questions during the debate

Agents never assume past a gap. A question about the code, an agent checks itself first. Anything it can't answer that way goes to the lead, which answers from the code or puts it to the user (one at a time), and the answer is sent to every agent it affects before round 2.

### Round 2: disagreements

The lead lists the material disagreements by point ID. Only the agents involved take part, continued with SendMessage. The lead takes part in any disagreement it has a position on, as one of the four. Each receives the brief, its own round 1 output, the opposing positions **word for word** (never the lead's summary) and any answered questions, and returns:

```
ROLE / LEVEL:
ON <ID>:      agree / disagree / revised, and why (one block per disputed point)
REC:          final recommendation (unchanged or revised)
NEW RISKS:    any raised by the other positions, with ID
```

Skip round 2 when there is no material disagreement.

### More than four agents

1. Group agents by related role (for example product + UX + frontend; architect + backend + data; security + DevOps + performance; QA + developer).
2. Run round 2 inside each group, four at most. A disagreement that crosses groups gets its own debate, between just the agents involved.
3. Every group's output still goes to the lead in full. The lead does not drop points because they came from a smaller group.

## Decision

The lead takes on every point raised: all specialist recommendations, the QA testability and risk assessment, developer implementation feedback, its own position, and every objection, agreement and revised position. Reviewer feedback comes after, on the draft (see Reviewer checks).

- **Where the team agrees**, that is the decision. The lead takes it on as it stands.
- **Where ideas still conflict after round 2**, the lead makes the final call, weighing reasoning quality, risk and relevance (not a vote), and records why in the ledger. Points it argued against still get a fair outcome.

The lead then drafts the final scope, final approach, rejected alternatives and why, acceptance criteria, test plan, risks accepted, open questions and the ticket list.

### The point ledger

The lead keeps one ledger of every point ID raised in either round. Each ends with exactly one outcome:

| Outcome | Meaning |
|---|---|
| Adopted | In the plan; names the ticket it goes in |
| Rejected | Not done; one-line reason |
| Risk accepted | Known and left; one-line reason |
| Open question | Still needs an answer; becomes a decision ticket |

A point with no outcome means the decision is not finished. The ledger goes to the reviewer at each check, and to the user at confirmation 2 (as a count per outcome, with the rejected and accepted ones listed).

## Reviewer checks

The reviewer is the independent check. It never argues a position in the debate, so it has nothing to defend when it judges the result. It is one agent, spawned at check 1 and continued with SendMessage for checks 2 and 3.

| Check | When | Looks at | Who fixes |
|---|---|---|---|
| 1. Draft decision | After round 2, before confirmation 2 | Gaps, contradictions, overbuilding; every ledger point has an outcome | The lead |
| 2. Tickets | Ticket stage, before posting | Every adopted point is in a ticket; each ticket stands on its own | The lead |
| 3. Code | After implementation | The pull request against the acceptance criteria and test plan; overbuilding | The main session |

At each check:

1. The reviewer reports findings with IDs (`REV-1`, `REV-2`), which go in the ledger.
2. The lead makes the change, or rejects the finding with a one-line reason.
3. If a finding reopens a specialist's area (for example a new security risk), the lead sends that one point to the specialists involved with SendMessage and gets a short answer. This is a question, not a third debate round.
4. The reviewer checks once more, looking only at what changed.
5. Anything still disputed goes to the user: listed at confirmation 2 as "reviewer says X, lead says Y" for checks 1 and 2, or as a ticket for check 3.

**One fix-and-recheck loop at most per check.** On Lite teams, which have no reviewer, the lead does checks 1 and 2 itself, and check 3 is the project's normal tests and checks.

## Ticket stage

Runs after confirmation 2, before implementation. Only the lead writes to GitHub. Agents only draft.

1. **The lead drafts each approved ticket in full**, in plain sentences: the problem and the plan, the files or component to change, acceptance criteria and tests (from QA), risks accepted, "Needs first" for tickets that depend on another, and a link to the main ticket that holds the decision. The main ticket is the one the brief came from; if there wasn't one, the lead creates it first, holding the decision and its reasons.
2. **The lead searches the open tickets** first and updates a matching one instead of creating a copy. One task per ticket.
3. **Reviewer check 2:** the reviewer checks the drafts against the decision and the point ledger, and the lead fixes them (see Reviewer checks).
4. **The lead posts the tickets** to the repo approved at confirmation 2, turns each open question into a decision ticket, and gives the user the links.

The debate itself never goes into a ticket: only the decision and its reasons. If the project does not use GitHub issues, the tickets stay in chat as the final plan.

## Confirmation gates

1. **Before the debate:** roles, agents per role, levels, QA, developer representative, reviewer, token estimate.
2. **Before the ticket stage and implementation:** the decision items above (after reviewer check 1), the point ledger summary, any reviewer disputes, and the ticket list (titles, one line each, and the repo they go to). This yes also covers posting those tickets.

Nothing starts without the user's yes at each gate.
