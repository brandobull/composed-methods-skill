---
name: composed-methods
description: Use for a focused readability review or behavior-preserving refactor of generated or existing code. Check composed methods, clear names, control flow, and resource ownership against the target project's language conventions and quality gates.
---

# Composed Methods

## Overview

Make an operation understandable from its entry point through its helpers. A reader should be able to explain its trigger, ordered steps, important decisions, resource ownership, and failure paths without the author's narration. This is a focused readability workflow, not a substitute for correctness, security, performance, or architecture review.

**Approval standard:** The result is easier to understand as a whole, follows the project's conventions, preserves behavior, and passes applicable checks. Shorter functions or a lower complexity score alone do not meet that standard.

## When to use

- After implementing a change, before final review or commit, when a focused readability pass would help.
- When reviewing generated code or a diff for composed methods and naming.
- When asked to refactor hard-to-follow code without changing behavior.

Use review-only mode unless edits are requested. Keep the scope to the requested code and the callers, helpers, and tests needed to judge it. If the code is already clear, report that and stop. Do not start a repository-wide cleanup from a focused review.

## Review workflow

### 1. Establish the local contract

Read repository instructions, style guides, relevant module documentation, nearby examples, and tests. Identify the changed entry points and their callers. Follow explicit project rules first, then established language conventions. For example, Python functions usually use `snake_case` and TypeScript functions usually use `camelCase` when the project agrees.

Find configured complexity, lint, type, and test checks. Record the project's actual threshold and command; do not impose a universal score or weaken a gate to make the code pass. If a check is absent, review the relevant quality manually and say what could not be measured.

### 2. Trace the operation

Read each entry point in execution order through its helpers and affected tests. Include error, cancellation, cleanup, and early-exit paths. Before suggesting a change, identify the behavior and constraints it must preserve.

Ask these questions of the whole call chain:

1. **Purpose and sequence:** Does the coordinating function read as ordered, clearly named steps? Are important ordering and conditions visible?
2. **Level of abstraction:** Does each helper explain one meaningful step? If a helper coordinates multiple steps, are they named at one consistent level?
3. **Control and ownership:** Can a reader see where state changes, side effects, resource acquisition and release, errors, and cancellation happen?
4. **Names and boundaries:** Do names expose actions, units, and valid states? Do module placement and exports match local conventions?
5. **Tests and comments:** Do tests communicate observable behavior or a documented contract? Do comments preserve non-obvious constraints and reasons?

Extract a meaningful step even with one caller. Stop decomposing when a function already expresses one cohesive operation with straightforward details. Simple calculations, loops, and conditions can remain inline. Prefer clear branches and early exits when they clarify the flow; do not hide ownership or ordering behind a predicate or add an async boundary merely to shorten a function.

### 3. Report actionable findings

For each material finding, give the file and line, the reading difficulty or risk, and a concrete remedy. Mark violations of explicit project rules and material comprehension problems as required; label subjective alternatives as optional. Review affected tests as code, too. If there are no material findings, state the scope reviewed and checks run.

## Repair workflow

1. Understand callers, behavior, edge cases, and side-effect order before editing. For untested legacy behavior, add a characterization test before restructuring when feasible. Do not rewrite existing tests merely to accommodate the refactor.
2. Make one coherent, scoped change at a time. Extract named steps, improve names, or simplify branches only where that reduces the mental work of following the operation. Preserve inputs, outputs, errors, cancellation, resource lifetimes, side-effect order, and performance-sensitive behavior.
3. Reread the entire operation after each meaningful extraction. Reverse a change that only moves complexity elsewhere or adds unnecessary indirection. Keep comments that explain why a constraint exists.
4. Run the focused tests, then the applicable project type, lint, and complexity checks. Run broader checks when a shared boundary changes. Inspect the final diff for unrelated edits and report any remaining uncertainty.

## Common failure modes

| Temptation | Better standard |
| --- | --- |
| Split every block into a helper | Name meaningful steps; keep straightforward details inline. |
| Move branches into vague predicates to satisfy a score | Make the decision and its consequences understandable at the call site. |
| Accept a passing complexity check as proof of clarity | Trace the whole operation, including errors, cleanup, and tests. |
| Refactor nearby code while already in the file | Limit changes to the requested behavior and necessary context. |
| Assume green tests prove a legacy refactor safe | Characterize uncovered behavior and inspect side effects and ordering. |

## Verification and handoff

Finish with the review scope or changed files, required findings addressed, exact checks run and their results, and any unverified behavior. A reviewer should be able to understand the result from the code and this evidence without relying on the implementer's explanation.

In an agent-skills workflow, apply local readability rules while building. Use this skill as a focused pass after implementation and focused tests; a broader code review still examines correctness and other risks. If an independent reviewer is requested, give that agent the code and relevant project instructions in review-only mode. The implementing agent addresses confirmed findings and reruns checks. Skill availability alone does not authorize edits or require another agent.
