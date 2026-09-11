---
name: ddd4j-boot-version-selection
description: Use when choosing a compatible ddd4j-boot maintenance line for a Spring Boot project, upgrade, or legacy system based on Spring Boot, ddd4j, JDK, Maven, and POM model constraints.
license: Apache-2.0
---

# ddd4j-boot Version Selection

## Overview

Spring Boot version and JDK are the entry points; the output is the complete Boot→ddd4j→JDK→Maven/POM tuple.

## Quick Matrix

| Boot | ddd4j | JDK | Maven/POM |
|---|---|---:|---|
| 2.3–2.7 | 1.0.x | 8 | Maven 3 / 4.0 |
| 3.0–3.5 | 2.0.x | 17 | Maven 3 / 4.0 |
| 4.0–4.1 | 3.0.x | 21 | Maven 4 / 4.1 |

For exact patches, see the [13 Maintenance Lines](references/maintenance-matrix.md).

## Decision Rules

1. Existing projects first respect the current Spring Boot/JDK.
2. New projects choose the highest primary combination the organization supports and that is remotely consumable.
3. Do not mix parent/BOM across ddd4j main lines.
4. Boot 4 requires Maven 4/POM 4.1/subprojects.
5. Output SOURCE/TEST/CI/PUBLISHED/CONSUMED evidence status.

## Capability Boundaries

### ✅ Strong At

- Selecting among the 13 maintenance lines.
- Upgrade paths and incompatibility explanations.
- JDK/Maven/POM constraints.
- Remote consumption gates.

### ⚠️ Needs Input

- Spring Boot/JDK/Maven.
- Current parent/BOM.
- Private repository and CI requirements.

### ❌ Out of Scope

- Automatically upgrading source code.
- Guessing unreleased coordinates.
- Using a local cache to prove remote availability.

## Deep Reference

- [Maintenance Matrix](references/maintenance-matrix.md)
- [Selection and Upgrade](references/selection-and-upgrade.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never output Maven settings or private repository credentials.

## Quick Start

- "Use `$ddd4j-boot-version-selection` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-boot-version-selection` to review existing usage against the current source."
- "Use `$ddd4j-boot-version-selection` to return an implementation choice, evidence state, and remaining risk."

## Audience and Customization

- Developers: provide the target maintenance line, POM, capabilities, and acceptance behavior.
- Architects: specify a read-only boundary review, compatibility, or migration target.
- Testers / release engineers: specify the required evidence levels; do not auto-expand to release or production operations.

Customize the target framework, allowed implementations, excluded modules, compatibility requirements, and output evidence level. When input is insufficient, give a tentative verdict first, then list "missing: specific item; how to provide: required path or configuration".

## FAQ

1. **Are skills organized by Maven artifact?** No — by the user-facing capability domain.
2. **Can I copy another maintenance line directly?** No — verify the version and source first.
3. **Does a class existing in source prove the capability works?** No — registration and behavior evidence are also required.
4. **How do I report tests that did not run?** Mark `NOT RUN` or `BLOCKED`.
5. **Can the skill commit or release automatically?** Only after explicit user authorization.
6. **What if the implementation is missing?** Describe the missing module or evidence; do not invent APIs.
