# Graphify for the engineering team

This file does not replace Graphify. Load the installed **`graphify`** skill and follow it for building and querying the graph. This file only says how the team uses the results.

## When

Before selecting specialist roles. The findings decide which roles are material, and each agent gets only the findings for its role.

## How

Use the installed skill's commands: `graphify query "<question>"`, `graphify path "<A>" "<B>"`, `graphify explain "<concept>"`. If the project has no graph yet, build one with that skill first. Read the code directly only when the graph doesn't answer the question.

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
