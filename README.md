# engineering-team

A [Claude Code](https://docs.claude.com/en/docs/claude-code) skill that runs your software planning like an engineering team.

You bring a brief, such as *"add magic-link login"* or *"move reporting off the main database"*. A **lead** takes it on, the way an engineering manager would. It asks you only what the brief leaves open, reads your codebase, and picks the right lineup of specialists for the job. You confirm the lineup before anyone starts. Then the team gets to work: the specialists debate, the lead decides, and an independent reviewer checks the result. Nothing is built until you approve the plan.

What you get back is a decision you can act on: the scope, the approach, what was rejected and why, acceptance criteria, a test plan, the risks being accepted, and tickets ready to build from.

## How it works

```mermaid
flowchart TD
    subgraph P1["1. Brief"]
        A["You give the lead a brief"] --> B{"Anything left open?"}
        B -- "yes" --> C["Lead asks you, one question at a time"]
        C --> B
    end

    subgraph P2["2. Lineup"]
        D["Lead reads the codebase"] --> E{"Is a team worth it?"}
        E -- "no" --> F["Lead does the work directly"]
        E -- "yes" --> G["Lead picks the lineup and estimates the cost"]
        G --> H{{"Checkpoint 1: you confirm the lineup"}}
        H -- "change it" --> G
    end

    subgraph P3["3. Work"]
        I["Each specialist writes an independent position"] --> J["QA adds tests to every proposed ticket"]
        J --> K{"Disagreement that matters?"}
        K -- "yes" --> L["Those involved respond to each other"]
        L --> M["Lead drafts the decision"]
        K -- "no" --> M
        M --> N["Reviewer checks the draft, lead fixes it"]
        N --> O{{"Checkpoint 2: you approve the plan"}}
        O -- "change it" --> M
        O -- "approve" --> Q["Lead writes the tickets, reviewer checks them"]
        Q --> R["Build on a branch and run the tests"]
        R --> S["Reviewer checks the pull request"]
        S --> T["You review and merge"]
    end

    B -- "no" --> D
    H -- "confirm" --> I
```

There are three phases, and the lead runs all of them:

1. **Brief.** The lead makes sure it understands what you want.
2. **Lineup.** The lead decides who is needed, and you confirm it.
3. **Work.** The team plans, the lead decides, you approve, and it's built.

## The problem it solves

Ask an assistant to plan a feature and you get one confident answer. It usually runs with however you framed the request, and it rarely pushes back. The gaps show up later, when they cost more to fix:

- **Blind spots surface during the build.** The migration that can't be rolled back, the permission check nobody thought of, the edge case with no test. A real team catches these in planning, because someone in the room is paid to worry about each one.
- **Plans overbuild.** A single planner tends to add layers, abstractions and dependencies "for later", when reusing what's already in the codebase would have done.
- **Nobody argues.** One viewpoint means no one asks "what if we didn't?" or "what breaks if this is slow?", so weak assumptions go unchallenged.
- **Decisions vanish.** The reasoning lives in a chat history. A week later, nobody remembers why an approach was chosen or what was ruled out.
- **You either micromanage or rubber-stamp.** You review every step yourself, or you approve a plan you haven't really checked.

This skill brings back what a good team does in a planning session: a lead who picks the right people, a short, structured disagreement, one person accountable for the decision, an independent review, and a written record that becomes the tickets.

## Requirements

- **[Claude Code](https://docs.claude.com/en/docs/claude-code).** That's all it needs.
- **[GitHub CLI](https://cli.github.com/)** (`gh`), signed in, if you want tickets created as GitHub issues and pull requests opened. Without it, the plan and tickets stay in the conversation.

### Recommended

Both are optional, but worth having in the projects where you use this skill:

- **[Graphify](https://pypi.org/project/graphifyy/)** (`pip install graphifyy`) builds a map of the repository, so the lead starts from how the code really fits together. Without it, the lead reads the code directly.
- **[Ponytail](https://github.com/DietrichGebert/ponytail)** pushes plans and code towards the smallest thing that works. Without it, the team still follows the same reuse-first rules, which are built into the skill.

## Install

Clone it into your Claude Code skills folder:

```sh
git clone https://github.com/SamNewhouse/engineering-team ~/.claude/skills/engineering-team
```

Restart Claude Code. `engineering-team` will appear in the skills list.

To update it later:

```sh
git -C ~/.claude/skills/engineering-team pull
```

## Usage

Open Claude Code in your project and hand the lead a brief:

```
/engineering-team Add CSV export to the orders page, keeping the current filters
```

You can also just describe the work. The skill picks up planning and design work that spans several areas or carries real risk.

**When it's worth using:** a feature that touches several parts of the system, anything involving payments, personal data, permissions or migrations, or a change with more than one sensible approach.

**When it isn't:** a one-file fix, a clear bug or a small edit. The lead notices this, says so, and just does the work.

## Each phase in detail

### Phase 1: Brief

The lead reads your brief and checks it has what it needs: the goal, any constraints, and what "done" means. If something is missing, it asks you, one question at a time. If the brief already covers it, it doesn't ask.

### Phase 2: Lineup

**The lead reads the codebase.** It works out what the change touches: modules and boundaries, dependencies between services, data flow, API contracts, shared components, gaps in test coverage, and deployment. It uses Graphify if you have it, and reads the code if not.

**The lead decides whether a team is worth it.** If the job turns out to be small with one obvious approach, it says so and does the work itself.

**The lead picks the lineup.** It chooses only the specialists the brief needs, sets a level for each member, adds the fixed roles (QA, a developer representative, and a reviewer for bigger teams), and estimates the token cost.

**Checkpoint 1: you confirm the lineup.** You see the team size, each role and its levels, and the estimated cost. Confirm it, or ask for changes. Nothing runs until you say yes.

### Phase 3: Work

**Independent positions.** Every specialist works alone, in parallel, and writes a recommendation, the reasoning, risks, assumptions, what would change its mind, any questions, and the tickets it would create for its area. If a specialist needs information, the lead finds the answer in the code or asks you. Nobody guesses.

**QA pass.** QA adds acceptance criteria and tests to every proposed ticket.

**Disagreements.** If specialists disagree on something that matters, only those involved see each other's positions, word for word, and respond. At most four debate at a time, and there's only one such round.

**The lead drafts the decision.** It weighs the arguments rather than counting votes. Every point raised gets exactly one outcome: **adopted**, **rejected** (with a reason), **risk accepted** (with a reason) or **open question**.

**The reviewer checks the draft.** The reviewer hasn't taken part in the debate, so it has no position to defend. It looks for gaps, contradictions, overbuilding and points left without an outcome. The lead makes the fixes. If a fix reopens a specialist's area, the lead asks that specialist directly.

**Checkpoint 2: you approve the plan.** You see the final scope and approach, the rejected alternatives, the acceptance criteria, the test plan, the risks accepted, the open questions, any point where the reviewer and the lead still disagree, and the list of tickets it will create. Approve it, or push back. Your yes also covers creating those tickets.

**Tickets.** The lead writes each ticket in full: the problem, the plan, which files to change, acceptance criteria and tests, and what it depends on. The reviewer checks that nothing from the decision was lost, then the tickets are posted as GitHub issues. Open questions become tickets of their own. The debate itself never goes into a ticket, only the decision and its reasons.

**Build.** The work is built on a new branch and the project's tests are run. The reviewer checks the pull request against the acceptance criteria. You get the pull request link to review and merge.

## The lineup

### Sizes

| Size | For | Members |
|---|---|---:|
| **Lite** | Small, low-risk changes with one real design choice | 3 |
| **Medium** | Normal feature work | 5 to 7 |
| **Large** | Complex, high-risk or multi-area work | 9 to 11 |

The lead isn't counted. Sizes stay odd where possible.

### Specialists

The lead chooses from these, based on the brief:

| Area | Specialists |
|---|---|
| Product and design | Product planner, UX planner |
| Building it | Systems architect, backend planner, frontend planner, data planner, integration planner |
| Running it safely | Security planner, DevOps planner, performance planner |
| After launch | Documentation planner, analytics planner |

A user-facing feature gets product, UX and frontend. A payments change gets security, data and architecture.

### Fixed roles

- **QA** is always in the lineup: one or two members, never junior. It owns the acceptance criteria and the test plan.
- **Developer representative** is always in the lineup. It speaks for whoever has to build and maintain the result.
- **Reviewer** joins medium and large lineups. It doesn't debate. It checks the draft decision, the tickets and the code.

### Levels

| Level | Model | Brings |
|---|---|---|
| Senior | Sonnet, or Opus for high-risk calls | Architecture, security, long-term trade-offs |
| Mid-level | Sonnet | Practical planning and delivery |
| Junior | Haiku | Challenging assumptions, spotting simple gaps |

A role has one to three members. A junior is only ever the third member of a role, never on its own.

### Example lineups

| Brief | Size | Lineup |
|---|---|---|
| Simple UI change | Medium, 5 | UX, frontend, developer representative, QA, reviewer (all mid-level) |
| New API endpoint with data changes | Medium, 7 | Product, architect, backend, data, developer representative, QA, reviewer |
| Complex backend migration | Large, 9 | 2 architects, 2 backend, data, developer representative, 2 QA, reviewer |
| Payments or personal data | Large, 9 | Product, architect, backend, data, security, developer representative, 2 QA, reviewer |

## Nothing gets lost

- **Every point has an ID**, such as `SEC-S1` (security, senior, point 1), so you can follow it from the debate to a ticket.
- **No second-hand summaries.** When specialists respond to each other, they see the opposing positions word for word.
- **Short notes, full facts.** Specialists write terse structured notes to save tokens, but every field is filled in, and file paths and numbers are copied exactly.
- **Every point ends with an outcome.** The decision isn't finished until it does, and the reviewer checks this.
- **The reviewer only checks.** It reports what it finds, the lead makes the changes, and anything still disputed comes to you.

## Cost

A team run uses many more tokens than a single conversation. Lite is cheapest and Large costs the most. You see an estimate for your brief at checkpoint 1, before anything runs. The figures the estimate is based on are in `rules/team-composition.md` and are worth adjusting once you've done a few runs.

## Customising

- **Roles** live in `roles/`, one short file each. Edit one to change its focus, or add a new role and list it in `SKILL.md`.
- **Team rules** (sizes, levels, the debate format, reviewer checks, tickets, cost estimates) live in `rules/team-composition.md`.

## Layout

```
engineering-team/
├── SKILL.md                   the workflow Claude Code follows
├── README.md
├── LICENSE
├── roles/                     one file per role
├── rules/team-composition.md  sizes, levels, debate, decision, reviewer, tickets
└── companions/
    ├── graphify.md            how the lead uses Graphify (or reads the code without it)
    └── ponytail.md            the reuse-first rules
```

## Licence

[MIT](LICENSE)
