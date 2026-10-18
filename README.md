# Composed Methods

A focused engineering skill for reviewing and improving code readability. It makes process entry points read as ordered steps, keeps helpers at a consistent level of abstraction, and keeps control flow and resource ownership apparent.

The workflow follows the production engineering pattern in [Addy Osmani's Agent Skills](https://github.com/addyosmani/agent-skills): explicit activation, project-context review, scoped repair, verification gates, and failure modes. It complements that collection's broader `code-review-and-quality` and `code-simplification` skills with a composed-method lens. This is an independent repository.

The skill reads each target repository's instructions before judging code. It follows that project's language conventions and configured complexity threshold, if any; it does not impose a universal style or score.

## Install

With the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add brandobull/composed-methods-skill
```

Or copy `skills/composed-methods/` into a skill directory recognized by your coding agent. The skill uses the [Agent Skills format](https://agentskills.io/specification) and has no agent-specific dependencies.

## Use

Ask your agent to use `composed-methods` for a focused pass. For example:

- “Review this diff with composed-methods. Report actionable readability findings; do not edit.”
- “Use composed-methods to refactor this module for clarity while preserving behavior.”
- “Have a separate agent review the generated code with composed-methods before final review.”

The skill starts in review-only mode unless edits are requested. Its repair workflow preserves behavior, uses characterization tests for untested legacy paths when feasible, runs the project's applicable checks, and reports the evidence. It belongs after implementation and focused tests and before the final broad review.

## Validate changes

Check the skill against the Agent Skills reference validator:

```bash
uvx --from skills-ref agentskills validate ./skills/composed-methods
```

After publishing, `npx skills add brandobull/composed-methods-skill --list` confirms that an installer discovers it.

## License

MIT. See [LICENSE](LICENSE).
