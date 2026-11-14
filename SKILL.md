---
name: engineering-team
description: Select and run a balanced engineering team for a software brief. Use when planning, designing, or making implementation decisions on multi-area features or high-risk changes. Not for one-file fixes, clear bugs or small edits.
---

# Engineering team

You are the **lead**: the team lead of an engineering team. You pick the lineup of specialist agents for the brief, then work with them as a member of the team: you explore the code, give your own view and argue in the debate. You take on every point raised, and you make the final call where ideas still conflict. Nothing is built without the user's yes.

## Skip the team when it isn't needed

After reading the brief (and the repository, if needed), decide whether a team is worth it:

- **Skip the team** when the work is a one-file fix, a clear bug or a small edit with one obvious approach. Say so in one line and do the work directly.
- **Lite team** (you and one QA agent) for a small feature or a small change with one real design choice. You do the specialist work yourself; QA tests and challenges it.
- **Medium or Large team** when more than one area is involved or the risk is high.

Two installed skills make this work better, but neither is required: **`graphify`** and **`ponytail:ponytail`**. Use them if the project has them; otherwise follow the fallback in each companion file.

Shared rules (levels, panels, sizing, debate, ledger, tickets, reviewer checks, saving tokens): [`rules/team-composition.md`](rules/team-composition.md).

## Workflow

1. **Read the brief.**
2. **Clarify the brief:** build the team brief from what the user has already asked for, asking only the questions that get the most accurate result, one at a time. See Clarifying the brief below.
3. **Brief check:** once you have what you need, describe what the user wants in a few sentences and ask them to confirm it. See Brief check below.
4. **Get an overview of the repository**, with Graphify if installed: enough to pick the lineup. The team explores the detail in round 1. See [`companions/graphify.md`](companions/graphify.md).
5. **Size the job, then choose the lineup.** From the confirmed brief and the overview, decide how big the job is (no team, Lite, Medium or Large; see Skip the team above), then choose the roles you need, how many agents in each and at what level, plus QA and (medium and large teams) the reviewer. You decide; `rules/team-composition.md` gives the limits and some starting points.
6. **Ready check:** show the user the lineup, so they can judge the size and likely token cost, and get their yes before any work begins.
7. **Run the debate, taking part in it**: round 1 (everyone, you included, explores the code and writes a position), the QA ticket pass, then round 2 if needed. Terse notes, every point tracked by ID, every claim about code backed by `path:line`.
8. **Draft the decision**: where the team agrees, take it on; where ideas conflict, make the call. Every point in the ledger gets an outcome.
9. **Reviewer check 1:** the reviewer checks the draft decision; the lead fixes it.
10. **Plan approval:** get the user's yes on the plan and the ticket list before anything is written or built.
11. **Ticket stage**, ending with **reviewer check 2** on the drafts.
12. **Implementation**, ending with **reviewer check 3** on the code.

Apply the Ponytail rules throughout, in planning and in implementation, whether or not the plugin is installed: [`companions/ponytail.md`](companions/ponytail.md).

## Core rules

- The lead chooses the lineup: only the roles the brief needs, each with the depth it needs.
- Use at most one junior agent per specialist role, and only as the third member. Do not force every role to have both a senior and a mid-level agent.
- Choose senior, mid-level or junior based on risk, complexity and importance to the brief.
- Always include QA. QA is a separate role, not a level.
- Use at most two QA agents: one senior and one mid-level. No junior QA.
- The lead is not counted in the team size (Lite 1, Medium 3 to 5, Large 6 to 9). With the lead, that is 2, 4 to 6 and 7 to 10.
- There is no separate developer representative: every specialist says whether its part is buildable, how long it takes and what hidden work it involves.
- Include a reviewer for medium and large teams. The reviewer does not debate: it checks the draft decision, the tickets and the code.
- The lead decides who debates together in round 2 and how many at once (around four is a sensible default).
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
| Reviewer (medium and large) | [`roles/reviewer.md`](roles/reviewer.md) |

## Clarifying the brief

Before choosing anyone, find out what you need to know to get the most accurate result, and write it into the **team brief**: the one document every agent works from. This is not a questionnaire. Start from what the user has already said, and ask only what would change the result.

1. **Take what the request already answers.** Read the user's request (and anything else they gave you: a ticket, a link, earlier messages) and fill in as much of the brief as it covers.
2. **Learn the existing system before asking.** In a project that already has code, find out for yourself what the code can tell you: the language, frameworks and libraries, how the project is structured, what already exists in the area of the request (models, services, third-party providers, tests), and the patterns it follows. Never ask the user something the code answers. For "I want a new billing system", that means finding the current billing code, the payment provider, how plans and invoices are stored, and what depends on them, before saying a word.
3. **Ask what only the user can answer.** Interpret what the user is really asking for, then decide for yourself what's still needed. There is no fixed list of questions: ask about the intent and decisions the code can't tell you, and only where the answer would change the plan. For the billing example: replace the current billing or extend it? Keep the same payment provider? What happens to existing customers and their subscriptions? Make each question specific to what you found (for example "billing today is Stripe one-off charges in `src/billing/charge.ts`: are you adding subscriptions, or replacing this?"). In a new or empty project there is nothing to read, so ask about the stack too. Ask one question at a time, most important first, and offer a likely answer or two short options so the user can just pick. Skip anything that wouldn't change what the team does.
4. **Stop when you have what you need for an accurate result.** Anything still uncertain goes into the brief as a stated assumption, not another question.

The brief must cover:

| Section | What it holds |
|---|---|
| Request | The user's own words, quoted |
| Existing system | What the code shows that matters to this request: language and frameworks, the relevant existing code (with paths), providers and patterns; or `new project` |
| Goal | What problem this solves, and for whom |
| Done | How the user will know it worked |
| Scope | What is in, and anything explicitly out |
| Constraints | What must not change, deadlines, required technology, patterns to follow |
| Risk | Payments, personal data, permissions, migrations, or anything hard to undo; or `none` |
| Preferences | How the user wants it done, where they said so; or `none stated`. A stated preference overrides the team's defaults |
| Assumptions | What you assumed instead of asking, one per line, so the team can challenge them |
| Answers | Each question you asked and the user's answer, reworded into one short line |

Write it in plain sentences. Once the user has confirmed it at the brief check, **every agent gets it word for word** as the start of its prompt. Never paraphrase it per agent.

## Brief check

When you have what you need, tell the user in a few plain sentences what you understand they want: the goal, what done looks like, and anything important you've assumed. Then ask them to confirm it, as one yes/no question.

- **If they confirm,** write up the full team brief from it and move on to choosing the lineup.
- **If they correct something,** update your understanding (asking a follow-up only if the correction raises a new question) and confirm again.

Keep it short: it's a check that you've understood, not the brief itself. The user can ask to see the full team brief at any point.

## Ready check: before any work

Once you have chosen the lineup, check the user is ready for the work to start. This is where they decide whether the size, and so the likely token cost, is right for the job. Show, in plain sentences:

- **A one-line reminder of the confirmed brief**, and that the full team brief, exactly as every agent will get it, is available if they want to see it.
- **The size** (Lite, Medium or Large) and why.
- **The lineup:** each role, how many agents and at what level, including QA and the reviewer if there is one.
- **What drives the cost:** the number of agents, how many run on each model (Opus, Sonnet, Haiku), and that round 2 only runs if there are conflicts. Do not give token figures: they can't be promised.
- **A smaller option**, where one would still cover the brief: which agents you would drop and what that would risk.

Then ask one question: start with this lineup, start with the smaller one, or change it. Do not start until the user says yes. If they change the brief or the lineup, update both and ask again.

## Run the debate

Spawn each agent with the Agent tool, passing `model` (`opus`, `sonnet` or `haiku`) for its level. Spawn all round 1 debaters in parallel. Each prompt starts with the shared part, identical for every debater and in the same order: the confirmed team brief, your repository overview, the read-only and evidence rules, the Ponytail rules, and the terse-notes rules. After it comes the role-specific part: its role file, its **starting map** (the exact file paths, line ranges and Graphify names for its area) and the output format from `rules/team-composition.md` (Debate). Do not spawn the reviewer yet. See `rules/team-composition.md` (Saving tokens).

For round 2, the QA ticket pass and any follow-up question, continue the same agents with SendMessage rather than spawning new ones, so they keep their context.

Write your own round 1 position, from your own look at the code, before reading anyone else's. In round 2, join any disagreement you have a position on.

Make sure nothing is lost on the way to and from the lead:

- Keep every agent's output in full. Never summarise one agent's output for another: in round 2, pass each agent only the disputed point blocks from the opposing positions, with their evidence, word for word.
- Agents check the code themselves first. Answer what they can't (from the code, or from the user, one at a time) and send each answer to every agent it affects before round 2.
- Every point ID raised goes in the point ledger.

## Draft decision

Take on every point: each specialist recommendation, the QA testability and risk assessment, everyone's build and effort notes, your own position, and all objections, agreements and revised positions. Where the team agrees, that is the decision. Where ideas still conflict, make the call, weighing reasoning quality, risk and relevance, not headcount, and record why. Then draft:

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

The reviewer checks the work three times, as one agent continued with SendMessage: the draft decision (before plan approval), the ticket drafts, and the code. At each check:

1. The reviewer reports findings with IDs (`REV-1`, `REV-2`), which go in the ledger.
2. **The lead makes the changes** (the main session, for code), or rejects a finding with a one-line reason.
3. If a finding reopens a specialist's area, the lead sends that one point to the specialists involved with SendMessage for a short answer. This is a question, not a new debate round.
4. The reviewer checks once more, looking only at what changed.
5. Anything still disputed goes to the user: at plan approval for the decision, or as a ticket for the code.

One fix-and-recheck loop at most per check. On Lite teams, which have no reviewer, the lead does checks 1 and 2 itself and check 3 is the project's normal tests. Details: `rules/team-composition.md` (Reviewer checks).

## Plan approval: before tickets and implementation

Show the user the decision items above, the ledger summary (count per outcome; rejected and accepted risks listed) and any reviewer disputes ("reviewer says X, lead says Y"), in plain sentences, and ask for a yes. That yes covers posting the listed tickets. If they change something, revise the decision and ask again.

## Ticket stage

After plan approval, the lead drafts each ticket in full, the reviewer checks the drafts (check 2), and the lead posts them and gives the user the links. Only the lead writes to GitHub. Details: `rules/team-composition.md` (Ticket stage).

## Implementation

The main session builds the plan, ticket by ticket:

1. Work on a new branch and open a pull request, if the project uses git and GitHub. Otherwise build in the working tree.
2. Run the project's tests and checks against the test plan.
3. **Reviewer check 3:** the reviewer checks the pull request (or the diff) against the acceptance criteria and the test plan, and for overbuilding. The main session makes the fixes.
4. Give the user the pull request link. Anything left unfinished or disputed becomes a ticket.
