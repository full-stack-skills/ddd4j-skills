# CLAUDE.md

## Project overview

`ddd4j-skills` is the source-aligned Agent Skills package for the ddd4j Java ecosystem. It is separate from generic `java-skills` and methodology-oriented `ddd-skills`.

## Authoritative source

Before changing API guidance, verify the current source and tests in the applicable ddd4j maintenance line. Do not infer cross-line parity from names. Current source checkouts may use CodeGraph; when `.codegraph/` exists, query it before text search.

## Structure

- `.claude-plugin/plugin.json`: package registry
- `skills/<skill-name>/SKILL.md`: entrypoint
- `skills/<skill-name>/references/`: source evidence and deep guidance
- `README.md` / `README.zh-CN.md`: bilingual package index

## Rules

- Keep every SKILL.md under 500 lines.
- Descriptions state when the skill applies and distinguish ddd4j from generic Java/framework usage.
- Preserve maintenance-line JDK, Maven, POM, dependency, and API contracts.
- Source review, tests, CI, publication, remote consumption, and production acceptance are separate evidence gates.
- Cross-skill handoffs use skill name plus install command, never sibling relative links.
- Update plugin registry and both READMEs whenever membership changes.
- Run frontmatter/link checks, source-contract checks, `git diff --check`, and TRACE before release.

