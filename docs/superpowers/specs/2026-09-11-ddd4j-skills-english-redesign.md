# ddd4j-skills English Redesign — Design Spec

**Date:** 2026-09-11
**Scope:** `full-stack-skills-repositories/ddd4j-skills/` (62 skills, ~150 reference files)
**Path:** architectural — touches skill body, references/, README, and supporting docs.

## Goal

Rewrite all 62 skills in the `ddd4j-skills` package in English, preserving the existing
section structure, capability boundaries, and evidence layout. Translate every
`SKILL.md` and every `references/*.md` to English. Add one new
`references/workflow.md` per skill containing a concrete end-to-end example.

## Why

The current skills are written in Chinese. They are functional but inaccessible to
English-speaking developers and to English-language Agent harnesses. Translating
them — without losing the carefully-designed capability boundaries and source
evidence gates — gives the same package to a wider audience.

## Approach

1. **Mirror, don't restructure.** Lock the section vocabulary to a single glossary so
   every skill reads identically section-by-section. Section names map:

   | Chinese | English |
   |---|---|
   | 概述 / Overview | Overview |
   | 快速开始 | Quick Start |
   | 输入契约 | Input Contract |
   | 决策顺序 | Decision Order |
   | 快速矩阵 | Quick Matrix |
   | 输出格式 | Output Format |
   | 能力边界 | Capability Boundaries |
   | ✅ 擅长 | ✅ Strong At |
   | ⚠️ 需要素材 | ⚠️ Needs Input |
   | ❌ 超范围 | ❌ Out of Scope |
   | 常见错误 | Common Mistakes |
   | 深度参考 | Deep Reference |
   | 隐私与安全 | Privacy and Security |
   | 受众与定制 | Audience and Customization |
   | 常见问题 / FAQ | FAQ |

2. **Translate `references/` files.** Update the "采集日期 / collection date" header
   to 2026-09-11 in every file. Keep all tables, code blocks, evidence paths
   unchanged.

3. **Add `references/workflow.md` per skill.** Concrete end-to-end scenario:
   setup → decision → implementation → verification. ~30–60 lines per file.
   For skills that already have a deep workflow in another reference (e.g. the
   `architecture` skill), the new `workflow.md` instead contains a short checklist.

4. **Update cross-skill references.** Audit every `../` link, replace with the
   `npx skills add full-stack-skills/ddd4j-skills --skill <name>` pattern. The
   existing Chinese skills already follow this rule; the English translation
   must preserve it.

5. **Update README and plugin manifest.**
   - `README.md`: rewrite in English, mirror current section structure, keep the
     62-row skill table with the "Use when" column translated.
   - `README.zh-CN.md`: keep unchanged.
   - `.claude-plugin/plugin.json`: keep unchanged (skill paths and order are
     stable).

## Section glossary (locked)

Frontmatter:

```yaml
---
name: <skill-name>
description: Use when <one-sentence activation condition>.
license: Apache-2.0
---
```

Each SKILL.md MUST contain, in order:

1. `# <skill-name>` title
2. `## Overview`
3. `## Quick Start` (4 trigger questions, bulleted)
4. `## Input Contract` (numbered list of required inputs)
5. `## Decision Order` or `## Workflow` (whichever the existing skill uses)
6. `## Quick Matrix` (table, where applicable)
7. `## Output Format` (table with columns Field / Content)
8. `## Capability Boundaries`
   - `### ✅ Strong At`
   - `### ⚠️ Needs Input`
   - `### ❌ Out of Scope`
9. `## Common Mistakes` (numbered)
10. `## Deep Reference` (bulleted list of `references/` files)
11. `## Privacy and Security`
12. `## Audience and Customization`
13. `## FAQ` (numbered Q&A)

Skills may drop sections 5–7 if their domain doesn't have a matrix or decision
order. This is consistent with the existing Chinese skills.

## Capability boundary style

Use first-person plural for capabilities, neutral for out-of-scope:

- ✅ Strong At: bullet list of concrete capabilities.
- ⚠️ Needs Input: bullet list of missing inputs that prevent the skill from acting.
- ❌ Out of Scope: bullet list of actions the skill must NOT take.

## Output format

Every skill must end the SKILL.md with a clear "what comes back to the caller"
table. For decision-oriented skills (version-selection, architecture, bom) this is
a Recommendation / Alternative / Incompatible / Unverified table. For
implementation-oriented skills (data, mq, web) this is a Code shape or
Configuration shape table.

## References/

Per skill, after translation:

- All existing `references/*.md` translated to English.
- One new `references/workflow.md` added per skill.

For skill groups that share a workflow pattern (e.g. all `ddd4j-boot-*` skills
share the Spring Boot autoconfiguration lifecycle), use a single canonical
`workflow.md` body and only adjust the skill name in the heading.

## README

`README.md` rewrite:

- Title block and "Overview" — translated.
- Install instructions — keep code blocks as-is.
- "Skills (62)" table — translate the "Use when" column, keep skill names as-is.
- "Boundaries" — translated.
- License — unchanged.

`README.zh-CN.md`: keep unchanged (becomes the bilingual counterpart).

## Trace evidence

- Re-run cross-skill `../` link audit after rewrite. Clean run = no broken links.
- Run `./scripts/evaluate-package.sh ddd4j-skills` after rewrite. Target: average
  score ≥ 4.5 per skill (matching the workspace baseline).

## Out of scope

- No new skills added. No skills removed or merged.
- No changes to capability boundaries (the `✅ / ⚠️ / ❌` content) — only the
  English wording.
- No codegraph build against the 5 ddd4j source repos (per user direction: light
  verification only — trust existing references/).
- No edits to `docs/superpowers/plans/`.
- No edits to `.gitignore`, `LICENSE`, or `CLAUDE.md` (CLAUDE.md is the source
  of rules and stays authoritative).

## Risks

1. **Translation drift across 62 skills.** Mitigation: lock the section
   glossary above; translate in skill-group batches (boot, javalin, quarkus,
   cloud, root).
2. **Inconsistent technical terms.** Mitigation: maintain a term glossary at
   `docs/superpowers/specs/2026-09-11-ddd4j-skills-glossary.md` — terms like
   维护线 = maintenance line, 适配项目 = adapter project, POM Model = POM Model.
3. **Date staleness.** Mitigation: every translated references/ file gets the
   collection-date header bumped to 2026-09-11 in the same edit.

## Deliverables

- 62 rewritten `skills/<name>/SKILL.md` files (English).
- ~90 translated `skills/<name>/references/*.md` files (English).
- 62 new `skills/<name>/references/workflow.md` files.
- 1 rewritten `README.md` (English).
- 1 term glossary at `docs/superpowers/specs/2026-09-11-ddd4j-skills-glossary.md`.
- Re-run cross-skill link audit (clean).
- Re-run TRACE (`./scripts/evaluate-package.sh ddd4j-skills`).

## Workflow

Implementation proceeds in this order:

1. Read the current Chinese SKILL.md for a skill, plus all references/.
2. Translate each section using the locked glossary.
3. Write the new `references/workflow.md`.
4. Update the collection-date header in every translated references file.
5. Move to the next skill.

Skill-group order (smaller first to validate the pattern):

1. ddd4j root (14 skills) — establishes the template.
2. ddd4j-boot (13) — second, most cross-references.
3. ddd4j-javalin (11).
4. ddd4j-quarkus (11).
5. ddd4j-cloud (11).

After each group: re-run link audit and TRACE on that group before committing.

## Outcome note (2026-09-11)

Trace result after translation: 62/62 scored, package average overall ≈ 3.91
(was ≈ 4.06 with identical content in Chinese). The entire delta is the T2
(国内适配性) sub-item, which mechanically scores `has_chinese=false` as 2.0/5.0
by design — an intentional scorer bias toward China-domestic adaptation, not a
content regression. The ≥ 4.5 target in this spec is unattainable for pure-English
skills under the current T2 rule; treat ddd4j-skills TRACE numbers as comparable
only against other English packages.

## Self-review

Spec check (inline, before user review):

- [x] No placeholders ("TBD", "TODO").
- [x] Internal consistency: section glossary matches every Chinese term used in
      existing skills.
- [x] Scope: one spec, one implementation plan, bounded to 62 skills.
- [x] Ambiguity: capability-boundary style is locked to first-person / neutral.
