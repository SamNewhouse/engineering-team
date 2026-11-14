# Graphify for the engineering team

Graphify is optional. If the **`graphify`** skill is installed, load it and follow it for building and querying the graph. If it isn't, read the code directly to find the same things. Either way, this file says what the team needs to know.

## When

Before selecting specialist roles. The findings decide which roles are material, and each agent gets only the findings for its role.

## How

- **With Graphify:** use `graphify query "<question>"`, `graphify path "<A>" "<B>"` and `graphify explain "<concept>"`. If the project has no graph yet, build one first. Read the code directly only when the graph doesn't answer the question.
- **Without Graphify:** search and read the code that the brief touches, and fill in the same table below. Say in the findings that they come from reading the code, so gaps are expected.

## What to find, and which roles it informs

| Finding | Informs |
|---|---|
| Existing modules and boundaries | Systems architect, backend planner, frontend planner, developer representative |
| Dependencies between services | Systems architect, integration planner, DevOps planner, performance planner |
| Data flow | Data planner, security planner, analytics planner, backend planner |
| API contracts | Backend planner, integration planner, frontend planner, documentation planner |
| Shared components | Frontend planner, UX planner, developer representative, reviewer |
| Test coverage gaps | QA, reviewer, developer representative |
| Deployment and infrastructure relationships | DevOps planner, security planner, performance planner |

The product planner gets a short summary of what already exists, so the scope builds on it.

## Output

A short list of findings under the seven headings above, each naming the files or modules involved.
