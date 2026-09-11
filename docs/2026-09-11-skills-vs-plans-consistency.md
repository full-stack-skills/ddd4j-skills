# Skills vs. Plans Consistency Check

**Date:** 2026-09-11
**Scope:** `ddd4j-skills` — 62 skills against the five plan documents in `docs/superpowers/plans/`.

## Method

1. Extracted the planned skill list from the "计划技能 / 规划基线" table in each of the
   five plan documents:
   - `2026-09-11-ddd4j-skills-plan.md` (root group)
   - `2026-09-11-ddd4j-boot-skills-plan.md`
   - `2026-09-11-ddd4j-javalin-skills-plan.md`
   - `2026-09-11-ddd4j-quarkus-skills-plan.md`
   - `2026-09-11-ddd4j-cloud-skills-plan.md`
2. Compared the planned names against `skills/` on disk.
3. For each skill, checked that the terms promised in the plan's "统一覆盖"
   column actually appear in the skill's `SKILL.md` or its `references/`.
4. Verified the package manifests (`plugin.json`, both READMEs) against disk.

## 1. Membership

| Group | Planned | On disk | Missing | Extra |
|---|---:|---:|---|---|
| root | 14 | 14 | — | — |
| boot | 13 | 13 | — | — |
| javalin | 12 | 12 | — | — |
| quarkus | 11 | 11 | — | — |
| cloud | 12 | 12 | — | — |
| **total** | **62** | **62** | **none** | **none** |

Every skill named in a plan exists on disk. No unplanned skill was added.

## 2. Content coverage

Each skill was scanned for the capabilities its plan promises. Result: **60 of 62
fully matched**.

Two flagged items were reviewed manually and resolved as **false positives**:

| Skill | Term not found | Resolution |
|---|---|---|
| `ddd4j-architecture` | "hexagonal" | The plan says 六边形 (hexagonal). The skill covers the same concept under its standard alternative name, "ports and adapters" — which is the same architectural pattern. Semantically covered. |
| `ddd4j-javalin-web` | "request size" | The skill's description and feature matrix say "request limits" and "limits", which is the same surface. Semantically covered. |

No substantive coverage gap was found.

## 3. Manifest consistency

| Artifact | Declared | Actual | Consistent |
|---|---:|---:|---|
| `.claude-plugin/plugin.json` | 62 | 62 | ✅ |
| `README.md` skill table rows | 62 | 62 | ✅ |
| `README.zh-CN.md` skill table rows | 62 | 62 | ✅ |

Section headings and ordering in `plugin.json` match the on-disk directory set exactly.

## 4. Plan constraints

| Plan constraint | Status |
|---|---|
| SKILL.md under 500 lines | ✅ (max 128 before optimization) |
| Detailed material in a single `references/` layer | ✅ (4–8 files per skill) |
| Cross-skill handoffs by name + install command, never `../` | ✅ (0 broken links) |
| Plugin registry and both READMEs updated on membership change | ✅ |
| Frontmatter/link checks, source-contract checks, `git diff --check` before release | ✅ |

## 5. Deviations from the plans (informational)

These are not gaps, but they differ from a literal reading of the plans:

1. **`docs/superpowers/specs/` was added.** The plans do not mention a specs
   directory. It was created during the 2026-09-11 English redesign
   (`2026-09-11-ddd4j-skills-english-redesign.md`, `2026-09-11-ddd4j-skills-glossary.md`).
   The plans live in `docs/superpowers/plans/`; the specs directory is a sibling.

2. **All 62 skills are written in English.** The plans were written in Chinese and
   do not specify a language. The English rewrite was a separate user decision on
   2026-09-11 and preserves the section structure the plans describe.

3. **Source code was not re-mined.** The plans state that skills should be verified
   against the current source in
   `/Users/wandl/workspaces/workspace-ddd4j/workspace-ddd4j-boot/` and
   `/Users/wandl/workspaces/workspace-ddd4j/workspace-ddd4j-cloud/`. The 2026-09-11
   rewrite used the existing `references/` evidence rather than re-reading source,
   by explicit user direction. The plans' "源码证据" claim is therefore inherited,
   not re-verified in this pass.

## Verdict

The 62 skills are **consistent with the plans** in membership, per-skill capability
coverage, and package manifests. The three deviations above are additive or
user-directed, not contradictions.
