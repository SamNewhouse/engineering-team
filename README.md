# engineering-team

A skill for [Claude Code](https://docs.claude.com/en/docs/claude-code) that plans a piece of software work the way a good team would: the right specialists look at the problem, they argue about it briefly, one person makes the call, and nothing gets built until you've said yes.

You give it a brief ("add magic-link login", "move reporting off the main database"). It reads your codebase, picks only the specialists the job needs, runs a short structured debate between them, and comes back with a decision: scope, approach, what was rejected and why, acceptance criteria, a test plan and the risks being accepted. Once you approve, it writes the GitHub issues and starts the work.

## Why

Asking one assistant for a plan gets you one point of view. Asking a crowd gets you noise. This sits in between:

- **Distinct roles.** A security planner, a data planner and a UX planner fail in different ways, so each one catches problems the others miss.
- **Mixed depth.** Each role can have senior, mid-level and junior members. Senior members reason about long-term trade-offs, mid-level members keep it practical, and a junior member asks the obvious question everyone skipped.
- **One decision-maker.** The lead weighs the arguments rather than counting votes, and has to account for every point raised.
- **You stay in control.** There are two checkpoints, and nothing runs past either without your approval.
- **It doesn't overbuild.** Every recommendation has to justify new code over reusing what's already there.

## Requirements

- [Claude Code](https://docs.claude.com/en/docs/claude-code). That's all it needs.
- [GitHub CLI](https://cli.github.com/) (`gh`), signed in, if you want tickets written to GitHub issues. Without it, the plan stays in the conversation.

### Recommended

Both are optional, but worth setting up in the projects where you use this skill:

- [Graphify](https://pypi.org/project/graphifyy/) (`pip install graphifyy`) builds a map of the repository, so the team starts from how the code actually fits together. Without it, the lead reads the code directly.
- [Ponytail](https://github.com/DietrichGebert/ponytail) pushes plans and code towards the smallest thing that works. Without it, the team still follows the same reuse-first rules, which are written into the skill.

## Install

Clone it into your skills folder:

```sh
git clone https://github.com/SamNewhouse/engineering-team ~/.claude/skills/engineering-team
```

Restart Claude Code and the skill will be listed.

## Usage

Start it by name with a brief:

```
/engineering-team Add CSV export to the orders page, with filters applied
```

Or just describe a piece of work that spans several areas or carries real risk. The skill triggers on planning and design work, and stays out of the way for one-file fixes and obvious bugs.

### What happens

1. **Brief.** It reads your brief and asks follow-up questions only if something important is unclear, one at a time.
2. **Repository map.** It maps (with Graphify, if you have it) the modules, data flow, API contracts, shared components, test gaps and infrastructure that the change touches.
3. **Team.** It picks the roles the brief needs, gives each one a mix of levels, and estimates the token cost.
4. **Checkpoint 1.** You see the team and the cost estimate, and approve or adjust them.
5. **Debate.** Each member writes an independent position. Where they disagree on something that matters, the people involved get one round to respond to each other.
6. **Decision.** The lead decides. Every point raised ends up adopted, rejected with a reason, accepted as a known risk, or listed as an open question.
7. **Checkpoint 2.** You see the decision and the list of tickets it plans to create, and approve or push back.
8. **Tickets.** The lead writes each ticket in full, the reviewer checks that nothing from the decision was lost, and they're posted to GitHub.
9. **Build.** Implementation starts.

## The team

### Sizes

| Size | For | Members |
|---|---|---:|
| Lite | Simple, low-risk changes | 3 |
| Medium | Normal feature work | 5 to 7 |
| Large | Complex, high-risk or multi-area work | 9 to 11 |

The lead isn't counted. Team sizes stay odd where possible.

### Roles

Specialists are chosen to fit the brief: product, UX, systems architecture, backend, frontend, data, integrations, security, DevOps, performance, documentation and analytics. A user-facing feature gets product, UX and frontend. A payments change gets security, data and architecture.

Three roles are fixed:

- **QA** is always there: one or two members, never junior. It owns the test plan and acceptance criteria.
- **Developer representative** is always there. It speaks for whoever has to build and maintain the result.
- **Reviewer** joins medium and large teams. It checks the plan as a whole, and later the tickets and the code.

### Levels

| Level | Model | Brings |
|---|---|---|
| Senior | Sonnet, or Opus for high-risk calls | Architecture, security, long-term trade-offs |
| Mid-level | Sonnet | Practical planning and delivery |
| Junior | Haiku | Challenging assumptions, spotting simple gaps |

A role can have up to three members, with at most one junior, and a junior never works alone.

### How the debate stays honest

- Members write short structured notes, which saves tokens. Every field has to be filled in, and file paths and numbers are copied exactly.
- Each point gets an ID, so you can trace it from the debate to a ticket.
- Nobody sees a summary of someone else's argument. Opposing positions are passed on word for word.
- Members can't guess their way past a gap. Questions go to the lead, which answers them from the code or asks you.
- At most four members debate at once, and there are two rounds at most.

## Customising

- **Roles** live in `roles/`, one short file each. Edit a role to change what it focuses on, or add a new one and list it in `SKILL.md`.
- **Team rules** (sizes, level mixes, the debate format, ticket rules) live in `rules/team-composition.md`.
- **Token estimates** in `rules/team-composition.md` are starting figures. Adjust them once you've seen a few real runs.

## Layout

```
engineering-team/
├── SKILL.md                   the workflow and core rules
├── README.md
├── roles/                     one file per role
├── rules/team-composition.md  sizes, levels, debate, decision, tickets
└── companions/
    ├── graphify.md            how the team uses Graphify
    └── ponytail.md            how the team uses Ponytail
```
