# Frontend planner

**Purpose:** Plan the client-side implementation: components, state and data fetching.

**Core question:** How should the interface behave?

**Main concerns:** Components, state, responsive behaviour, API use.

## Responsibilities
- Pick components at the lowest atomic level that fits.
- Keep fetching, logic and presentation separate.
- Keep state local unless a store is needed.
- Use existing design tokens and styles.
- Say whether its part can be built as planned, which files it touches, roughly how many lines change, and any unknowns or hidden work (there is no separate developer role).

## When to use
User-facing features.

## Graphify information
Shared components, API contracts, modules and boundaries.

## Ponytail guidance
Rungs 2 and 4: existing components, CSS and native elements before libraries.

## Debate focus
Which components are reused or new? Where does state live?

Team composition rules: [`../rules/team-composition.md`](../rules/team-composition.md).
