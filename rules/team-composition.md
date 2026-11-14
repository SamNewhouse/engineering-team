# Team composition

Shared rules for every engineering-team run. The entry point is [`../SKILL.md`](../SKILL.md).

**Roles define responsibility. Levels define depth.** A role is what an agent is responsible for (systems architect, QA, reviewer). A level is how deep that agent goes (senior, mid-level, junior). Distinct roles stop the team converging on one view; mixed levels add diversity without forcing seniority.

## Capability levels

| Level | Model | Purpose |
|---|---|---|
| Senior | Sonnet, or Opus for high-risk decisions | Deep reasoning, architecture, security, long-term trade-offs |
| Mid-level | Sonnet | Practical planning, implementation, assurance, review |
| Junior | Haiku | Cheap, broad coverage: scanning a wide area for simple gaps |

The lead chooses the mix from:

- The risk and complexity of the work.
- The importance of the role to the brief.
- The need for architectural depth versus practical delivery input.
- The need for cheap, broad coverage of a wide area (the case for a junior).

Use Opus only for senior agents on high-risk decisions.

## The lead chooses the lineup

The lead decides who it needs: which roles, how many agents in each, and at what level. The rules below are the few limits it works within. Everything else in this section is guidance to help it choose, not a checklist.

**Fixed limits:**

- QA is always on the team: at most two agents, one senior and one mid-level. **No junior QA.**
- A reviewer joins medium and large teams: one agent, mid-level normally, senior for high-risk, architectural or security-sensitive work. It does not debate (see Reviewer checks).
- At most one junior per specialist role, and only as the third member.
- The total fits one of the sizes below.

Within those limits, the lead also decides how many agents debate together in round 2 (see Grouping the debate).

QA is a role, not a level. Role files hold the details: [`../roles/qa.md`](../roles/qa.md), [`../roles/reviewer.md`](../roles/reviewer.md).

**Building it is everyone's concern.** There is no separate developer representative: the specialists are the developers. Each one says whether its part is buildable as written, how long it will take, and what hidden work it involves.

## Team sizing

**The lead is not counted in these sizes.** It is the main session, not a spawned agent, but it is a full member of the team and takes part in the debate. The reviewer is counted but does not debate.

| Size | Use for | Agents | With the lead | Specialist agents | QA | Reviewer |
|---|---|---:|---:|---:|---:|---:|
| Lite | Small features and low-risk changes with one real design choice | 2 | 3 | 1 | 1 | 0 |
| Medium | Normal feature work | 3 to 5 | 4 to 6 | 1 to 3 | 1 or 2 | 1 |
| Large | Complex, high-risk or multi-area work | 6 to 9 | 7 to 10 | 3 to 6 | 2 | 1 |

**Lite is the lead, one specialist and one QA agent.** The lead picks the specialist for the area the change sits in (for example backend for an API tweak, frontend for a UI one), usually at mid-level, so the approach is always argued by two engineers. QA tests and challenges the plan. Where they conflict, they argue it out once and the lead makes the call.

The lead sizes the job after the brief check, from the confirmed brief and its overview of the code. Pick the smallest size that covers the brief. Work with no real design choice (a one-file fix, a clear bug, a small edit) gets no team at all.

## Choosing roles

Select only the roles that are material to the brief. These are common starting points, not rules; the lead adds or drops roles based on what its overview of the code shows:

| If the brief involves… | Usually needs |
|---|---|
| User-facing feature | Product, UX, frontend |
| Business logic or API | Product, systems architect, backend |
| Database or reporting | Data planner, systems architect |
| Third-party integration | Integration planner, backend |
| Authentication or sensitive data | Security planner, systems architect |
| Deployment or infrastructure | DevOps planner, systems architect |
| Performance-sensitive work | Performance planner, systems architect |
| Public-facing documentation | Documentation planner, product planner |
| Success measurement | Analytics planner, product planner |

QA is added to every team on top of these.

## Choosing levels

For each selected role, the lead picks one to three agents: senior or mid-level in any mix, with a junior allowed only as the third (below). Do not force every role to have both a senior and a mid-level agent: one mid-level agent is often enough. Give a role more depth when it carries more of the risk.

**Juniors:** at most one per role, and only as the third member, never alone or as one of the first two.

## Examples

Starting points, not fixed lineups. Each count is a range: the lead picks where in it to land from what the code shows, and can add or drop roles. Every example stays inside its size.

**Small feature** (add a filter to an existing list) — Lite, 2 agents plus the lead.

| Role | Level | Count |
|---|---|---:|
| Frontend planner | Mid-level | 1 |
| QA | Mid-level | 1 |

**UI change across several screens** — Medium, 4 to 5 agents. No senior is needed when the risk is low.

| Role | Level | Count |
|---|---|---:|
| UX planner | Mid-level | 1 |
| Frontend planner | Mid-level | 1 to 2 |
| QA | Mid-level | 1 |
| Reviewer | Mid-level | 1 |

**Backend API feature** (new endpoint with business rules and data changes) — Medium, 4 to 5 agents.

| Role | Level | Count |
|---|---|---:|
| Backend planner | Senior | 1 |
| Data planner | Mid-level | 1 |
| Systems architect | Mid-level, if the endpoint crosses service boundaries | 0 to 1 |
| QA | Senior | 1 |
| Reviewer | Mid-level | 1 |

**Complex backend migration** — Large, 6 to 9 agents, with strong architectural and data depth.

| Role | Level | Count |
|---|---|---:|
| Systems architect | Senior (Opus), plus a second senior if needed | 1 to 2 |
| Backend planner | Senior, plus mid-level if needed | 1 to 2 |
| Data planner | Senior (Opus), plus mid-level if needed | 1 to 2 |
| QA | Senior, mid-level | 2 |
| Reviewer | Senior | 1 |

**Payments or sensitive data** (payments, personal data, permissions, regulated workflows) — Large, 7 to 9 agents.

| Role | Level | Count |
|---|---|---:|
| Product planner | Senior, if scope or user impact is unclear | 0 to 1 |
| Systems architect | Senior | 1 |
| Backend planner | Mid-level | 1 |
| Data planner | Senior (Opus) | 1 |
| Security planner | Senior (Opus), plus mid-level if needed | 1 to 2 |
| QA | Senior, mid-level | 2 |
| Reviewer | Senior | 1 |

## Debate

**Two rounds at most.** The lead is a member of the team: it explores the code, writes its own round 1 position and takes part in round 2. Round 1 runs every debater in parallel. In round 2, the lead decides who debates together and how many at once. The reviewer does not debate. Every agent's output goes back to the lead in full. Nothing is summarised away between an agent and the lead.

### Saving tokens

Ways the team keeps its token use down, without losing any facts:

- **A starting map from the lead**: exact paths and line ranges for each debater, so nobody searches for what the lead has already found.
- **Line ranges, not whole files**, when reading code.
- **Only the disputed points in round 2**, word for word, instead of everyone's full round 1 output.
- **Continued agents**: round 2, the QA pass and the reviewer checks continue the same agents with SendMessage, so nothing is re-sent.
- **A shared prompt opening, for caching.** Every debater's prompt starts with the same shared part, identical word for word and in the same order: the confirmed team brief, the lead's overview, then the shared rules. The role-specific part (role file, starting map, output format) comes after. Repeated openings can be served from the prompt cache on requests to the same model. How much this saves is not measured.
- **Terse notes** (below) between agents and the lead.
- **Juniors for breadth**: a junior runs on Haiku and scans its area for simple gaps, rather than reasoning deeply about it.

### Terse notes

Agents write for the lead, not for people, so they use short notes instead of prose: fragments, no filler, no restating the brief. Terse means fewer words, never fewer facts:

- Every field in the format below is present, every time. Nothing to say → `none`. Don't know → `unknown: <what is missing>`.
- Every risk, assumption, objection and question is its own line. Never merge two into one.
- File paths, function names, numbers, versions and error text are copied exactly.
- Each point gets an ID made of the role, the level letter (`S`, `M` or `J`) and a number, such as `SEC-S1`, `SEC-M1` or `QA-S3`, so two agents in the same role never clash. The lead uses `LEAD-1`, `LEAD-2`; the reviewer uses `REV-1`, `REV-2`.

Tickets and anything shown to the user are written in plain sentences, not notes.

### Exploring the code

The team reads the code, not just the lead. In round 1, every debater (the lead included) explores the parts of the codebase its role covers:

1. **Start from the starting map.** From its overview, the lead gives each debater the exact file paths, line ranges and Graphify node or community names for its area (for example `src/auth/session.ts:20-80` and the `auth` community). Debaters begin there instead of searching.
2. Query Graphify (if installed) or search only for what the map doesn't cover: `graphify query`, `graphify path`, `graphify explain`. [`../companions/graphify.md`](../companions/graphify.md) says which areas each role covers.
3. **Read line ranges, not whole files.** Open the lines the map or the graph points to, and read further only when the argument needs it.
4. **Read-only.** Nobody changes code during the debate. Building starts after plan approval.
5. **Evidence for every claim.** Any statement about existing code cites where it comes from, such as `src/auth.ts:42`. Anything not checked is marked `unchecked`, so the reviewer can see which claims have nothing behind them.

### Round 1: independent positions

Each debater works alone, from the team brief, the lead's overview, its own exploration of the code, its role file and the Ponytail rules. **The lead writes its own position before reading anyone else's**, so it doesn't anchor on theirs. Each returns:

```
ROLE / LEVEL:
REC:          recommendation, and which Ponytail step it stops at
WHY:          reasoning
RISKS:        one per line, with ID
ASSUMES:      one per line, with ID
EVIDENCE:     path:line for each claim about existing code; `unchecked` where not checked
CHANGE-MIND:  what would change the recommendation
QUESTIONS:    anything it needs answered, one per line, with ID
BUILD:        is its part buildable as written; effort in concrete units; hidden work
TICKETS:      proposed tickets for its area: task, files or component, done means
```

### QA ticket pass

After round 1, the lead sends every agent's proposed tickets to the QA agents (continued with SendMessage). QA returns acceptance criteria and tests for each proposed ticket, with IDs. This is not a debate round: QA adds to the tickets, it does not argue positions. Any disagreement QA raises goes into round 2.

### Questions during the debate

Agents never assume past a gap. A question about the code, an agent checks itself first. Anything it can't answer that way goes to the lead, which answers from the code or puts it to the user (one at a time), and the answer is sent to every agent it affects before round 2.

### Round 2: disagreements

The lead lists the material disagreements by point ID. Only the agents involved take part, continued with SendMessage. The lead takes part in any disagreement it has a position on. Because each agent is continued, it already has the brief and its own round 1 output. It receives only the disputed point blocks from the opposing positions, with their evidence, **word for word** (never the lead's summary), plus any answered questions, and returns:

```
ROLE / LEVEL:
ON <ID>:      agree / disagree / revised, and why (one block per disputed point)
REC:          final recommendation (unchanged or revised)
NEW RISKS:    any raised by the other positions, with ID
```

Skip round 2 when there is no material disagreement.

### Grouping the debate

The lead decides how round 2 is grouped and how many agents debate at once. Small groups keep a debate focused, so around four at a time is a sensible default, but the lead can go higher or lower to fit the disagreement.

1. Group agents by related role (for example product + UX + frontend; architect + backend + data; security + DevOps + performance; QA + the specialists whose tickets it is testing).
2. Run round 2 inside each group. A disagreement that crosses groups gets its own debate, between just the agents involved.
3. Every group's output still goes to the lead in full. The lead does not drop points because they came from a smaller group.

## Decision

The lead takes on every point raised: all specialist recommendations, the QA testability and risk assessment, everyone's build and effort notes, its own position, and every objection, agreement and revised position. Reviewer feedback comes after, on the draft (see Reviewer checks).

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

A point with no outcome means the decision is not finished. The ledger goes to the reviewer at each check, and to the user at plan approval (as a count per outcome, with the rejected and accepted ones listed).

## Reviewer checks

The reviewer is the independent check. It never argues a position in the debate, so it has nothing to defend when it judges the result. It is one agent, spawned at check 1 and continued with SendMessage for checks 2 and 3.

| Check | When | Looks at | Who fixes |
|---|---|---|---|
| 1. Draft decision | After round 2, before plan approval | Gaps, contradictions, overbuilding; every ledger point has an outcome | The lead |
| 2. Tickets | Ticket stage, before posting | Every adopted point is in a ticket; each ticket stands on its own | The lead |
| 3. Code | After implementation | The pull request against the acceptance criteria and test plan; overbuilding | The main session |

At each check:

1. The reviewer reports findings with IDs (`REV-1`, `REV-2`), which go in the ledger.
2. The lead makes the change, or rejects the finding with a one-line reason.
3. If a finding reopens a specialist's area (for example a new security risk), the lead sends that one point to the specialists involved with SendMessage and gets a short answer. This is a question, not a third debate round.
4. The reviewer checks once more, looking only at what changed.
5. Anything still disputed goes to the user: listed at plan approval as "reviewer says X, lead says Y" for checks 1 and 2, or as a ticket for check 3.

**One fix-and-recheck loop at most per check.** On Lite teams, which have no reviewer, the lead does checks 1 and 2 itself, and check 3 is the project's normal tests and checks.

## Ticket stage

Runs after plan approval, before implementation. Only the lead writes to GitHub. Agents only draft.

1. **The lead drafts each approved ticket in full**, in plain sentences: the problem and the plan, the files or component to change, acceptance criteria and tests (from QA), risks accepted, "Needs first" for tickets that depend on another, and a link to the main ticket that holds the decision. The main ticket is the one the request came from; if there wasn't one, the lead creates it first, holding the decision and its reasons.
2. **The lead searches the open tickets** first and updates a matching one instead of creating a copy. One task per ticket.
3. **Reviewer check 2:** the reviewer checks the drafts against the decision and the point ledger, and the lead fixes them (see Reviewer checks).
4. **The lead posts the tickets** to the repo approved at plan approval, turns each open question into a decision ticket, and gives the user the links.

The debate itself never goes into a ticket: only the decision and its reasons. If the project does not use GitHub issues, the tickets stay in chat as the final plan.

## Confirmation gates

1. **Brief check, before choosing the lineup:** a few sentences on what the user wants (goal, done, key assumptions), confirmed as a yes/no.
2. **Ready check, before any work:** a reminder of the confirmed brief, the size, the lineup (roles, agents per role, levels, QA, reviewer), what drives the cost (agent count and models), and a smaller option where one fits. No token figures.
3. **Plan approval, before the ticket stage and implementation:** the decision items above (after reviewer check 1), the point ledger summary, any reviewer disputes, and the ticket list (titles, one line each, and the repo they go to). This yes also covers posting those tickets.

Nothing starts without the user's yes at each gate.
