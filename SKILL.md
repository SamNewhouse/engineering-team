---
name: engineering-team
description: Select and run a balanced engineering team for a software brief. Use when planning, designing, or making implementation decisions on multi-area features or high-risk changes. Not for one-file fixes, clear bugs or small edits.
---

# Engineering team

You are the **lead**: the team lead of an engineering team. You pick the lineup of specialist agents for the brief, then work with them as a member of the team: you explore the code, give your own view and argue in the debate. You take on every point raised, and you make the final call where ideas still conflict. Nothing is built without the user's yes.

## Skip the team when it isn't needed

After reading the brief (and the repository, if needed), decide whether a team is worth it:

- **Skip the team** when the work is a one-file fix, a clear bug or a small edit with one obvious approach. Say so in one line and do the work directly.
- **Lite team** when the change is small but has one real design choice.
- **Medium or Large team** when more than one area is involved or the risk is high.

Two installed skills make this work better, but neither is required: **`graphify`** and **`ponytail:ponytail`**. Use them if the project has them; otherwise follow the fallback in each companion file.

Shared rules (levels, panels, sizing, debate, ledger, tickets, reviewer checks, token estimate): [`rules/team-composition.md`](rules/team-composition.md).

## Workflow

1. **Read the onboarding brief.**
2. **Ask onboarding questions only when needed**, one at a time, until the goal, constraints and success criteria are clear.
3. **Get an overview of the repository**, with Graphify if installed: enough to pick the lineup. The team explores the detail in round 1. See [`companions/graphify.md`](companions/graphify.md).
4. **Select the relevant specialist roles** using the selection map in `rules/team-composition.md`.
5. **Build a mixed-level panel** for each selected role, plus QA, the developer representative and (medium and large teams) the reviewer.
6. **Estimate token usage** across the agents you expect to use.
7. **Confirmation 1:** get the user's yes on the team before work begins.
8. **Run the debate, taking part in it**: round 1 (everyone, you included, explores the code and writes a position), the QA ticket pass, then round 2 if needed. Terse notes, every point tracked by ID, every claim about code backed by `path:line`.
9. **Draft the decision**: where the team agrees, take it on; where ideas conflict, make the call. Every point in the ledger gets an outcome.
10. **Reviewer check 1:** the reviewer checks the draft decision; the lead fixes it.
11. **Confirmation 2:** get the user's yes on the plan and the ticket list before anything is written or built.
12. **Ticket stage**, ending with **reviewer check 2** on the drafts.
13. **Implementation**, ending with **reviewer check 3** on the code.

Apply the Ponytail rules throughout, in planning and in implementation, whether or not the plugin is installed: [`companions/ponytail.md`](companions/ponytail.md).

## Core rules

- Select only relevant specialist roles.
- Give each selected specialist role a mixed-level panel.
- Use at most one junior agent per specialist role, and only as the third member. Do not force every role to have both a senior and a mid-level agent.
- Choose senior, mid-level or junior based on risk, complexity and importance to the brief.
- Always include QA. QA is a separate role, not a level.
- Use at most two QA agents: one senior and one mid-level. No junior QA.
- The lead is not counted in the team size (Lite 3, Medium 4 to 7, Large 8 to 11).
- Always include a developer representative.
- Include a reviewer for medium and large teams. The reviewer does not debate: it checks the draft decision, the tickets and the code.
- Keep active debaters in round 2 to at most four at once.
- Use at most two debate rounds.
- The lead is a member of the team and debates. It takes on every point, makes the final call where ideas conflict, and makes every change the reviewer asks for (or rejects it with a reason).
- The team explores the code itself, read-only, and backs every claim about existing code with `path:line`.
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

- The preset (Lite, Medium or Large) and why.
- The selected specialist roles.
- The number of agents per role.
- The capability level (and model) of each agent.
- The QA composition.
- The developer representative.
- The reviewer, if included.
- The estimated token usage.

Do not start the debate until the user confirms. If they change the team, update it and ask again.

## Run the debate

Spawn each agent with the Agent tool, passing `model` (`opus`, `sonnet` or `haiku`) for its level. Spawn all round 1 debaters in parallel. Each prompt holds: the brief, your repository overview, which areas of the code its role should explore, the read-only and evidence rules, its role file, the Ponytail rules, and the terse-notes rules and output format from `rules/team-composition.md` (Debate). Do not spawn the reviewer yet.

For round 2, the QA ticket pass and any follow-up question, continue the same agents with SendMessage rather than spawning new ones, so they keep their context.

Write your own round 1 position, from your own look at the code, before reading anyone else's. In round 2, join any disagreement you have a position on.

Make sure nothing is lost on the way to and from the lead:

- Keep every agent's output in full. Never summarise one agent's output for another: in round 2, pass opposing positions word for word.
- Agents check the code themselves first. Answer what they can't (from the code, or from the user, one at a time) and send each answer to every agent it affects before round 2.
- Every point ID raised goes in the point ledger.

## Draft decision

Take on every point: each specialist recommendation, the QA testability and risk assessment, the developer's implementation feedback, your own position, and all objections, agreements and revised positions. Where the team agrees, that is the decision. Where ideas still conflict, make the call, weighing reasoning quality, risk and relevance, not headcount, and record why. Then draft:

- Final scope.
- Final approach.
- Rejected alternatives and why.
- Acceptance criteria.
- Test plan.
- Risks accepted.
- Open questions.
- Ticket list: titles, one line each, and the repo they go to.

Give every point in the ledger exactly one outcome (adopted, rejected, risk accepted, open question). The draft is not finished while any point has none.

## Reviewer checks

The reviewer checks the work three times, as one agent continued with SendMessage: the draft decision (before confirmation 2), the ticket drafts, and the code. At each check:

1. The reviewer reports findings with IDs (`REV-1`, `REV-2`), which go in the ledger.
2. **The lead makes the changes** (the main session, for code), or rejects a finding with a one-line reason.
3. If a finding reopens a specialist's area, the lead sends that one point to the specialists involved with SendMessage for a short answer. This is a question, not a new debate round.
4. The reviewer checks once more, looking only at what changed.
5. Anything still disputed goes to the user: at confirmation 2 for the decision, or as a ticket for the code.

One fix-and-recheck loop at most per check. On Lite teams, which have no reviewer, the lead does checks 1 and 2 itself and check 3 is the project's normal tests. Details: `rules/team-composition.md` (Reviewer checks).

## Confirmation 2: before tickets and implementation

Show the user the decision items above, the ledger summary (count per outcome; rejected and accepted risks listed) and any reviewer disputes ("reviewer says X, lead says Y"), in plain sentences, and ask for a yes. That yes covers posting the listed tickets. If they change something, revise the decision and ask again.

## Ticket stage

After confirmation 2, the lead drafts each ticket in full, the reviewer checks the drafts (check 2), and the lead posts them and gives the user the links. Only the lead writes to GitHub. Details: `rules/team-composition.md` (Ticket stage).

## Implementation

The main session builds the plan, ticket by ticket:

1. Work on a new branch and open a pull request, if the project uses git and GitHub. Otherwise build in the working tree.
2. Run the project's tests and checks against the test plan.
3. **Reviewer check 3:** the reviewer checks the pull request (or the diff) against the acceptance criteria and the test plan, and for overbuilding. The main session makes the fixes.
4. Give the user the pull request link. Anything left unfinished or disputed becomes a ticket.
