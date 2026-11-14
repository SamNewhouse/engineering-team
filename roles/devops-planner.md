# DevOps planner

**Purpose:** Plan deployment, infrastructure and operability.

**Core question:** How will it run and be operated?

**Main concerns:** Environments, CI/CD, deployment, monitoring, rollback.

## Responsibilities
- Plan build, deploy and rollback.
- Name config and environment changes.
- Plan monitoring and alerts that matter.
- Keep infrastructure changes minimal.
- Say whether its part can be built as planned, the effort in concrete units, and any hidden work (there is no separate developer role).

## When to use
Deployment or infrastructure.

## Graphify information
Deployment and infrastructure relationships, service dependencies.

## Ponytail guidance
Rung 4: managed platform features before custom infrastructure.

## Debate focus
Can it deploy and roll back safely? What needs doing by hand?

## Always check
Check each of these against the code. Report each one that applies as a RISKS line; leave out the rest.
- Every new environment variable or secret, and where it is set in each environment.
- Deploy order when code, schema or services change together.
- Rollback: what to run, and whether data changes survive it.
- Steps done by hand, each named in a ticket.
- CI runs the new tests and checks.
- Logs and alerts for each new failure mode.

Team composition rules: [`../rules/team-composition.md`](../rules/team-composition.md).
