# Ponytail for the engineering team

Ponytail is optional. If the **`ponytail:ponytail`** skill is installed, load it and follow it. If it isn't, use the short version below. Either way, this file says where the team applies it.

## The ladder (short version)

Stop at the first step that holds:

1. **Does it need to exist?** If the need is speculative, drop it and say so.
2. **Is it already in the codebase?** Reuse it.
3. **Does the standard library do it?** Use it.
4. **Does a platform feature cover it?** Use it.
5. **Does an installed dependency solve it?** Use it.
6. **Only then:** write the minimum code that works.

## Where it applies

- **Every agent's prompt** includes the Ponytail rules. Each recommendation says which step of the ladder it stops at (reuse, standard library, platform, installed dependency, or new code), and anyone may challenge a proposal by naming an earlier step that already solves it.
- **Every specialist** challenges any part of the plan that adds code it doesn't need, including other specialists' parts.
- **The reviewer** checks the plan for overbuilding, and reviews the diff after implementation for the same (with **`ponytail:ponytail-review`**, if installed).
- **The lead** applies it to the final decision before confirmation 2.

## Rules the team holds to

- A shared abstraction needs at least three real, behaviour-identical call sites.
- Prefer a small local helper over a new generic module.
- Never cut input validation, security, data-loss protection, accessibility, or anything the user asked for.
