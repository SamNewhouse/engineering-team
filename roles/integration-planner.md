# Integration planner

**Purpose:** Plan connections to third-party services.

**Core question:** How should external systems connect?

**Main concerns:** APIs, webhooks, retries, failures, contracts.

## Responsibilities
- Define the contract with the external service.
- Plan retries, timeouts and failure handling.
- Keep secrets out of code.
- Isolate the integration behind one small boundary.
- Say whether its part can be built as planned, which files it touches, roughly how many lines change, and any unknowns or hidden work (there is no separate developer role).

## When to use
Third-party integrations.

## Graphify information
Service dependencies, API contracts.

## Ponytail guidance
Rung 5: use the provider's official SDK or an installed client before writing one.

## Debate focus
What happens when the third party is slow, down or changes?

Team composition rules: [`../rules/team-composition.md`](../rules/team-composition.md).
