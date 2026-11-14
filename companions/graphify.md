# Graphify for the engineering team

Graphify is optional. If the **`graphify`** skill is installed, load it and follow it for building and querying the graph. If it isn't, read the code directly to find the same things. Either way, this file says what the team needs to know.

## When

Three times:

1. **The lead, while clarifying the request:** a quick look at the area the user is asking about (language, frameworks, existing code, providers), so it never asks what the code can answer.
2. **The lead, after the brief check:** an overview, enough to size the job, pick the lineup and write each debater's starting map. Not a deep read.
3. **Every debater, in round 1:** targeted queries into its own area, then the files the graph points to. The table below says which findings matter to which role. The lead explores too, for its own position.

## How

- **With Graphify:** use `graphify query "<question>"`, `graphify path "<A>" "<B>"` and `graphify explain "<concept>"`. If the project has no graph yet, build one first. Read the code directly only when the graph doesn't answer the question.
- **Without Graphify:** search and read the code that the request touches, and fill in the same table below. Say in the findings that they come from reading the code, so gaps are expected.

## What to find, and which roles it informs

| Finding | Informs |
|---|---|
| Existing modules and boundaries | Systems architect, backend planner, frontend planner |
| Dependencies between services | Systems architect, integration planner, DevOps planner, performance planner |
| Data flow | Data planner, security planner, analytics planner, backend planner |
| API contracts | Backend planner, integration planner, frontend planner, documentation planner |
| Shared components | Frontend planner, UX planner, reviewer |
| Test coverage gaps | QA, reviewer |
| Deployment and infrastructure relationships | DevOps planner, security planner, performance planner |

The product planner gets a short summary of what already exists, so the scope builds on it.

## Output

- **The lead's overview:** a short list under the seven headings above, naming the areas involved. It goes to every debater.
- **A starting map for each debater:** the exact file paths, line ranges and Graphify node or community names for that debater's area, taken from the overview, so it can start reading straight away instead of searching.
- **A debater's exploration:** goes into its own round 1 position, with `path:line` evidence for each claim.
