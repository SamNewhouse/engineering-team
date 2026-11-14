# Ponytail for the engineering team

This file does not replace Ponytail. Load the installed **`ponytail:ponytail`** skill and follow its ladder and rules. This file only says where the team applies it.

## Where it applies

- **Every agent's prompt** includes the Ponytail rules. Each recommendation says which step of the ladder it stops at (reuse, standard library, platform, installed dependency, or new code), and anyone may challenge a proposal by naming an earlier step that already solves it.
- **The developer representative** challenges any part of the plan that adds code it doesn't need.
- **The reviewer** checks the plan for overbuilding, and uses **`ponytail:ponytail-review`** on the diff after implementation.
- **The lead** applies it to the final decision before confirmation 2.

## Rules the team holds to

- A shared abstraction needs at least three real, behaviour-identical call sites.
- Prefer a small local helper over a new generic module.
- Never cut input validation, security, data-loss protection, accessibility, or anything the user asked for.
