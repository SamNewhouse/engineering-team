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
| 3 | Any mix of senior and mid-level, plus at most one junior |

Add more senior or mid-level agents only when more depth is needed. **Never more than one junior per specialist role.** Do not force every role to have both a senior and a mid-level agent: one mid-level agent is often enough.

| Senior | Mid-level | Junior | Valid? |
|---:|---:|---:|---|
| 1 | 0 | 0 | Yes |
| 0 | 1 | 0 | Yes |
| 1 | 1 | 0 | Yes |
| 2 | 0 | 0 | Yes |
| 1 | 1 | 1 | Yes |
| 0 | 2 | 1 | Yes |
| 0 | 0 | 1 | No: a junior never works alone |
| 0 | 0 | 2 | No: two juniors |
| 0 | 1 | 2 | No: two juniors |

## Always-present roles

| Role | When | Composition |
|---|---|---|
| QA | Always | At most two: one senior and one mid-level. **No junior QA.** |
| Developer representative | Always | One mid-level; senior for high-risk, architectural or security-sensitive work. |
| Reviewer | Medium and large teams | One mid-level; senior for high-risk, architectural or security-sensitive work. |

QA is a role, not a level. Use more than one developer representative or reviewer only when the brief genuinely needs separate perspectives. Role files hold the details: [`../roles/qa.md`](../roles/qa.md), [`../roles/developer-representative.md`](../roles/developer-representative.md), [`../roles/reviewer.md`](../roles/reviewer.md).

## Team sizing

**The lead is not counted.** It is the main session, not a spawned agent.

| Preset | Use for | Total | Specialist agents | QA | Developer rep | Reviewer |
|---|---|---:|---:|---:|---:|---:|
| Lite | Simple, low-risk changes | 3 | 1 | 1 | 1 | 0 |
| Medium | Normal feature work | 5 to 7 | 2 to 4 | 1 or 2 | 1 | 1 |
| Large | Complex, high-risk or multi-area work | 9 to 11 | 5 to 7 | 2 | 1 | 1 |

Pick the smallest preset that covers the brief. Keep the total odd: if a count lands on an even number, drop the least material agent, or add a junior challenger to a role that has room.

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

1. Read the approved brief and the Graphify findings.
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

Estimate = (agents × per-round cost × rounds expected) + Graphify pass (~10k) + lead synthesis (~15k) + ticket stage (~2–3k per ticket, plus ~15–20k for the reviewer check on medium and large teams). Round 2 only includes agents in a material disagreement, so count them separately. Give the user one total and the per-agent breakdown. These figures are first guesses: correct them after real runs.

## Debate

**Two rounds at most. Four active debaters at most at once.** Every agent's output goes back to the lead in full. Nothing is summarised away between an agent and the lead.

### Terse notes

Agents write for the lead, not for people, so they use short notes instead of prose: fragments, no filler, no restating the brief. Terse means fewer words, never fewer facts:

- Every field in the format below is present, every time. Nothing to say → `none`. Don't know → `unknown: <what is missing>`.
- Every risk, assumption, objection and question is its own line. Never merge two into one.
- File paths, function names, numbers, versions and error text are copied exactly.
- Each point gets an ID from the role and a number (`SEC-1`, `QA-3`), so it can be tracked to the end.

Tickets and anything shown to the user are written in plain sentences, not notes.

### Round 1: independent positions

Each agent works alone, from the brief, its Graphify findings, its role file and the Ponytail rules, and returns:

```
ROLE / LEVEL:
REC:          recommendation, and which Ponytail step it stops at
WHY:          reasoning
RISKS:        one per line, with ID
ASSUMES:      one per line, with ID
CHANGE-MIND:  what would change the recommendation
QUESTIONS:    anything it needs answered, one per line, with ID
TICKETS:      proposed tickets for its area: task, files or component, done means
```

QA also adds acceptance criteria and tests to each proposed ticket it can see, once round 1 is in.

### Questions during the debate

Agents never assume past a gap. A question is answered by the lead from the graph or the code, or put to the user (one at a time), and the answer is sent to every agent it affects before round 2.

### Round 2: disagreements

The lead lists the material disagreements by point ID. Only the agents involved take part. Each receives the brief, its own round 1 output, the opposing positions **word for word** (never the lead's summary) and any answered questions, and returns:

```
ROLE / LEVEL:
ON <ID>:      agree / disagree / revised, and why (one block per disputed point)
REC:          final recommendation (unchanged or revised)
NEW RISKS:    any raised by the other positions, with ID
```

Skip round 2 when there is no material disagreement.

### More than four agents

1. Group agents by related role (for example product + UX + frontend; architect + backend + data; security + DevOps + performance; QA + developer + reviewer).
2. Run round 2 inside each group, four at most. A disagreement that crosses groups gets its own debate, between just the agents involved.
3. Every group's output still goes to the lead in full. The lead does not drop points because they came from a smaller group.

## Lead decision

The lead receives all specialist recommendations, the QA testability and risk assessment, developer implementation feedback, reviewer quality and risk feedback, and every objection, agreement and revised position.

The lead weighs reasoning quality, risk and relevance (not a vote) and decides the final scope, final approach, rejected alternatives and why, acceptance criteria, test plan, risks accepted, open questions and the ticket list.

### The point ledger

The lead keeps one ledger of every point ID raised in either round. Each ends with exactly one outcome:

| Outcome | Meaning |
|---|---|
| Adopted | In the plan; names the ticket it goes in |
| Rejected | Not done; one-line reason |
| Risk accepted | Known and left; one-line reason |
| Open question | Still needs an answer; becomes a decision ticket |

A point with no outcome means the decision is not finished. The ledger goes to the user at confirmation 2 (as a count per outcome, with the rejected and accepted ones listed) and to the reviewer at the ticket stage.

## Ticket stage

Runs after confirmation 2, before implementation. Only the lead writes to GitHub. Agents only draft.

1. **The lead drafts each approved ticket in full**, in plain sentences: the problem and the plan, the files or component to change, acceptance criteria and tests (from QA), risks accepted, "Needs first" for tickets that depend on another, and a link to the main ticket that holds the decision.
2. **The lead searches the open tickets** first and updates a matching one instead of creating a copy. One task per ticket.
3. **The reviewer checks the drafts** against the decision and the point ledger: every adopted point is in a ticket, and each ticket can be picked up without the debate. On Lite teams, which have no reviewer, the lead does this check itself.
4. **The lead posts the tickets** to the repo approved at confirmation 2, turns each open question into a decision ticket, and gives the user the links.

The debate itself never goes into a ticket: only the decision and its reasons. If the project does not use GitHub issues, the tickets stay in chat as the final plan.

## Confirmation gates

1. **Before the debate:** roles, agents per role, levels, QA, developer representative, reviewer, token estimate.
2. **Before the ticket stage and implementation:** the decision items above, the point ledger summary, and the ticket list (titles, one line each, and the repo they go to). This yes also covers posting those tickets.

Nothing starts without the user's yes at each gate.
