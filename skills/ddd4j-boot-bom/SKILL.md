---
name: ddd4j-boot-bom
description: Use when managing ddd4j-boot parent, dependencies, BOM imports, effective POMs, version ownership, Spring Boot dependency alignment, Maven model, or consumer coordinates.
license: Apache-2.0
---

# ddd4j-boot BOM

## Overview

Targets the current ddd4j-boot maintenance line: boot-parent, boot-dependencies, boot-bom, the Spring Boot BOM, the ddd4j BOM, and effective POMs. Confirm the version line first, then apply this skill.

## Core Scope

boot-parent, boot-dependencies, boot-bom, Spring Boot BOM, ddd4j BOM, effective POM.

## Rules

1. Ordinary third-party versions are governed by ddd4j-dependencies; the Boot layer only overrides the Boot ecosystem.
2. BOM import order must be verified with an effective POM.
3. Boot 4 uses Maven 4/POM 4.1.
4. Concrete modules must not re-pin already-managed versions.
5. parent/BOM/aggregator POMs are different responsibilities.

## Capability Boundaries

### ✅ Strong At

- Boot-specific architecture and configuration decisions for the current line.
- Choosing among multiple implementations and dividing responsibilities.
- Maintenance-line differences and verification paths.

### ⚠️ Needs Input

- Target Boot line, JDK, Maven, and POM.
- Target module and runtime behavior.
- Current source/tests/CI status.

### ❌ Out of Scope

- Rewriting ddd4j core domain contracts.
- Treating dependency presence as runtime success.
- Automatically releasing or upgrading production projects.

## Workflow

1. Run ddd4j-boot-version-selection.
2. Read the target line's POMs, source, AutoConfiguration, and tests.
3. Compare candidate implementations and clarify default/override/degradation.
4. Execute target context or behavior tests.
5. Report source, test, CI, and publish evidence separately.

## Output and Exceptions

Output the version line, modules, configuration entry points, default implementations, override points, tests, and risks. When input is missing, write "missing: target line or module; how to provide: supply the POM and behavior requirements".

## Deep Reference

- [Source Evidence](references/source-evidence.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never output settings, tokens, passwords, or production connection information.

## Quick Start

- "Use `$ddd4j-boot-bom` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-boot-bom` to review existing usage against the current source."
- "Use `$ddd4j-boot-bom` to return an implementation choice, evidence state, and remaining risk."

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
