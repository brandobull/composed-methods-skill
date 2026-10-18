---
name: composed-methods
description: Review and improve code for composed methods, clear naming, and a consistent level of abstraction. Use for a focused readability review or behavior-preserving style refactor of generated or existing code, adapting to the target language and repository conventions.
---

# Composed Methods

Make an operation easy to understand from its entry point through its helpers. Use this skill to review code, or to improve it when edits are requested. Preserve the author's intended behavior and the project's conventions.

## When to use

- Review a diff, pull request, or module for readability after implementation.
- Improve code whose steps, names, or control flow are difficult to follow.
- Give a separate reviewer a focused style pass before a broader code review.

Keep the pass within the requested scope and the nearby code needed to understand it. If the code is already clear, report that without manufacturing changes.

## Establish the local standard

Read the repository's instructions, style guides, relevant module documentation, tests, and nearby examples. Explicit project rules take priority; otherwise follow the language's established conventions. For example, use `snake_case` for Python functions or `camelCase` for TypeScript functions when those match the target project.

Find any configured complexity threshold and its check. Run the check when relevant, but do not invent a universal threshold or change a gate to make a refactor pass. A passing score does not prove that the code is readable.

## Review from the entry point

Check whether a reader can identify:

1. **Purpose and sequence:** The coordinating function shows meaningful steps in the order they happen.
2. **Level of abstraction:** Each helper explains how one named step works; a helper that coordinates several steps names those substeps at one consistent level.
3. **Control and ownership:** Important conditions, errors, cancellation, side effects, and resource lifetimes remain visible where they affect the operation.
4. **Names and boundaries:** Names express actions, side effects, units, and valid states. Exports and module placement follow local conventions.
5. **Tests and comments:** Tests communicate observable behavior or a documented contract. Comments explain constraints and reasons that code alone cannot show.

Extract a meaningful step even if it has one caller. Stop when the current function already expresses one straightforward operation. Prefer clear branches, early exits, and named predicates where they reduce mental work. Avoid trivial wrappers, extra classes, vague helpers, or scattered files created only to shorten functions or lower a score. Include affected tests in the readability review.

For each material finding, cite the location, explain what makes the code hard to follow, and propose a concrete change. Distinguish a violated project rule from an optional suggestion. If there are no material findings, state the scope reviewed and checks run.

## Improve without changing behavior

Before editing, understand callers, current behavior, edge cases, tests, and the order of side effects. If legacy behavior lacks a safety net, add a characterization test when feasible. Make the smallest coherent change and preserve inputs, outputs, errors, cancellation, resource ownership, and performance-sensitive behavior.

Run focused tests and applicable type, lint, and complexity checks. Then reread the whole operation: the refactor should take fewer mental steps to understand, not merely contain shorter functions. Report remaining findings and anything that could not be verified.

## Fit into an agent workflow

Apply the project's readability rules while writing code. Use this skill for an explicit review or repair pass after implementation and focused tests, before final review or commit. An automated complexity gate complements this pass; it cannot judge whether the operation communicates its intent.

When an independent review is requested, give the reviewer the code and relevant project instructions with a review-only task. Let the implementing agent address confirmed findings, then rerun focused checks. The presence of this skill alone does not authorize edits or require another agent.
