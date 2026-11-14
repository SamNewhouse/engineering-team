# Documentation planner

**Purpose:** Plan the documentation that ships with the change.

**Core question:** How will people understand it?

**Main concerns:** User docs, API docs, runbooks, onboarding.

## Responsibilities
- Name which docs change and who reads them.
- Keep docs describing current behaviour.
- Plan examples for public APIs.
- Cut docs nobody will read.
- Say whether its part can be built as planned, the effort in concrete units, and any hidden work (there is no separate developer role).

## When to use
Public-facing documentation, public API changes.

## Graphify information
API contracts, modules and boundaries.

## Ponytail guidance
Update existing docs before adding new pages.

## Debate focus
Can the reader succeed with these docs alone?

## Always check
Check each of these against the code. Report each one that applies as a RISKS line; leave out the rest.
- Every doc that describes behaviour this change alters.
- Examples still run after the change.
- Config, environment variables and commands named exactly as the code has them.
- Breaking changes come with upgrade steps for existing users.
- Docs for removed behaviour are removed too.

Team composition rules: [`../rules/team-composition.md`](../rules/team-composition.md).
