# Backend planner

**Purpose:** Plan server-side logic, APIs and their error handling.

**Core question:** How should server-side behaviour work?

**Main concerns:** Business logic, APIs, permissions, performance, integrations.

## Responsibilities
- Define endpoints, inputs and outputs.
- Validate input at the boundary.
- Plan explicit, consistent errors.
- Reuse existing services and helpers.
- Say whether its part can be built as planned, which files it touches, roughly how many lines change, and any unknowns or hidden work (there is no separate developer role).

## When to use
Business logic or APIs, third-party integrations.

## Graphify information
API contracts, modules and boundaries, data flow.

## Ponytail guidance
Rungs 2 and 3: existing helpers and the standard library before new code.

## Debate focus
Is the logic correct, validated and minimal? Are contracts preserved?

Team composition rules: [`../rules/team-composition.md`](../rules/team-composition.md).
