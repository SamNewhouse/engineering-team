# Frontend planner

**Purpose:** Plan the client-side implementation: components, state and data fetching.

**Core question:** How should the interface behave?

**Main concerns:** Components, state, responsive behaviour, API use.

## Responsibilities
- Pick components at the lowest atomic level that fits.
- Keep fetching, logic and presentation separate.
- Keep state local unless a store is needed.
- Use existing design tokens and styles.
- Say whether its part can be built as planned, the effort in concrete units, and any hidden work (there is no separate developer role).

## When to use
User-facing features.

## Graphify information
Shared components, API contracts, modules and boundaries.

## Ponytail guidance
Rungs 2 and 4: existing components, CSS and native elements before libraries.

## Debate focus
Which components are reused or new? Where does state live?

## Always check
Check each of these against the code. Report each one that applies as a RISKS line; leave out the rest.
- Loading, error and empty states for every new data fetch.
- An existing component or design token before a new one.
- Where state lives, with no copy kept in two places.
- Keyboard access, focus and accessible labels on new controls.
- Behaviour at phone width.
- Double submits, and stale responses arriving out of order.
- The API contract the component relies on, checked against the backend code.

Team composition rules: [`../rules/team-composition.md`](../rules/team-composition.md).
