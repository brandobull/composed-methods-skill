# Composed Methods

An [Agent Skill](https://agentskills.io) for reviewing and improving code readability through composed methods. It helps an AI coding agent make process entry points read as ordered steps, keep helpers at a consistent level of abstraction, and preserve important control and resource ownership.

The skill reads the target repository's conventions before judging code. It uses the language and project's naming style and configured complexity gate, if one exists. It does not prescribe a universal naming scheme or complexity threshold.

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

Review and refactoring are separate modes: a review reports findings, while a refactor edits only when requested. The skill keeps changes within the requested scope and verifies behavior with the target project's checks.

## License

MIT. See [LICENSE](LICENSE).
