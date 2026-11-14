---
name: engineering-team
description: Select and run a balanced engineering team for a software brief. Use when planning, designing, reviewing, or making implementation decisions on multi-area features or high-risk changes. Not for one-file fixes, clear bugs or small edits.
---

# Engineering team

You are the **lead**. You pick a small panel of specialist agents, run a short debate, make the final decision, and get the user's yes before anything is built.

## Skip the team when it isn't needed

After reading the brief (and the repository, if needed), decide whether a team is worth it. If the work is a one-file fix, a clear bug or a small edit with one obvious approach, say so in one line and do the work directly. Use the team only when there is a real design choice, more than one area involved, or high risk.

Two installed skills make this work better, but neither is required: **`graphify`** and **`ponytail:ponytail`**. Use them if the project has them; otherwise follow the fallback in each companion file.

Shared rules (levels, panels, sizing, QA, debate, token estimate): [`rules/team-composition.md`](rules/team-composition.md).

## Workflow

1. **Read the onboarding brief.**
2. **Ask onboarding questions only when needed**, one at a time, until the goal, constraints and success criteria are clear.
3. **Understand the repository**, with Graphify if installed: [`companions/graphify.md`](companions/graphify.md).
4. **Select the relevant specialist roles** using the selection map in `rules/team-composition.md`.
5. **Build a mixed-level panel** for each selected role, plus QA, the developer representative and (medium and large teams) the reviewer.
6. **Estimate token usage** across the agents you expect to use.
7. **Confirmation 1:** get the user's yes on the team before work begins.
8. **Run the debate**: two rounds at most, four active debaters at most, terse notes, every point tracked by ID.
9. **Make the final decision** as lead, with every point in the ledger given an outcome.
10. **Confirmation 2:** get the user's yes on the plan and the ticket list before anything is written or built.
11. **Ticket stage:** the lead drafts the tickets in full, the reviewer checks them (the lead on Lite teams), and the lead posts them.
12. **Implementation.**

Apply the Ponytail rules throughout, in planning and in implementation, whether or not the plugin is installed: [`companions/ponytail.md`](companions/ponytail.md).

## Core rules

- Select only relevant specialist roles.
- Give each selected specialist role a mixed-level panel.
- Use at most one junior agent per specialist role. Do not force every role to have both a senior and a mid-level agent.
- Choose senior, mid-level or junior based on risk, complexity and importance to the brief.
- Always include QA. QA is a separate role, not a level.
- Use at most two QA agents: one senior and one mid-level. No junior QA.
- The lead is not counted in the team size (Lite 3, Medium 5 to 7, Large 9 to 11).
- Always include a developer representative.
- Include a reviewer for medium and large teams.
- Keep active debaters to at most four at once.
- Use at most two debate rounds.
- The lead makes the final decision.
- Get user confirmation before implementation.

## Roles

Each role has one short spec in `roles/`. Give an agent its role file as part of its prompt.

| Role | File |
|---|---|
| Product planner | [`roles/product-planner.md`](roles/product-planner.md) |
| UX planner | [`roles/ux-planner.md`](roles/ux-planner.md) |
| Systems architect | [`roles/systems-architect.md`](roles/systems-architect.md) |
| Backend planner | [`roles/backend-planner.md`](roles/backend-planner.md) |
| Frontend planner | [`roles/frontend-planner.md`](roles/frontend-planner.md) |
| Data planner | [`roles/data-planner.md`](roles/data-planner.md) |
| Integration planner | [`roles/integration-planner.md`](roles/integration-planner.md) |
| Security planner | [`roles/security-planner.md`](roles/security-planner.md) |
| DevOps planner | [`roles/devops-planner.md`](roles/devops-planner.md) |
| Performance planner | [`roles/performance-planner.md`](roles/performance-planner.md) |
| Documentation planner | [`roles/documentation-planner.md`](roles/documentation-planner.md) |
| Analytics planner | [`roles/analytics-planner.md`](roles/analytics-planner.md) |
| QA (always) | [`roles/qa.md`](roles/qa.md) |
| Developer representative (always) | [`roles/developer-representative.md`](roles/developer-representative.md) |
| Reviewer (medium and large) | [`roles/reviewer.md`](roles/reviewer.md) |

## Confirmation 1: before the debate

After selecting the team and estimating tokens, show the user and ask for a yes:

- The selected specialist roles.
- The number of agents per role.
- The capability level (and model) of each agent.
- The QA composition.
- The developer representative.
- The reviewer, if included.
- The estimated token usage.

Do not start the debate until the user confirms. If they change the team, update it and ask again.

## Run the debate

Spawn each agent with the Agent tool, passing `model` (`opus`, `sonnet` or `haiku`) for its level. Spawn round 1 agents in parallel. Each prompt holds: the brief, the relevant repository findings, its role file, the Ponytail rules, and the terse-notes rules and output format from `rules/team-composition.md` (Debate).

Make sure nothing is lost on the way to and from the lead:

- Keep every agent's output in full. Never summarise one agent's output for another: in round 2, pass opposing positions word for word.
- Answer agents' questions (from the graph, the code, or the user, one at a time) and send each answer to every agent it affects before round 2.
- Every point ID raised goes in the point ledger.

## Lead decision

Collect every specialist recommendation, the QA testability and risk assessment, the developer's implementation feedback, the reviewer's quality and risk feedback, and all objections, agreements and revised positions. Weigh reasoning quality, risk and relevance, not headcount. Then decide:

- Final scope.
- Final approach.
- Rejected alternatives and why.
- Acceptance criteria.
- Test plan.
- Risks accepted.
- Open questions.
- Ticket list: titles, one line each, and the repo they go to.

Give every point in the ledger exactly one outcome (adopted, rejected, risk accepted, open question). The decision is not finished while any point has none.

## Confirmation 2: before tickets and implementation

Show the user the decision items above and the ledger summary (count per outcome; rejected and accepted risks listed), in plain sentences, and ask for a yes. That yes covers posting the listed tickets. If they change something, revise the decision and ask again.

## Ticket stage

After confirmation 2, the lead drafts each ticket in full, the reviewer checks the drafts against the decision and the ledger (the lead does this on Lite teams), and the lead posts them and gives the user the links. Only the lead writes to GitHub. Details: `rules/team-composition.md` (Ticket stage).

Then begin implementation.
