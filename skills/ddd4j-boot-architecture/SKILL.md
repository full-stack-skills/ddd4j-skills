---
name: ddd4j-boot-architecture
description: Use when designing or reviewing ddd4j-boot module boundaries, parent/BOM layering, Spring Boot integration responsibilities, starter aggregation, or dependencies between core, auth, data, MQ, Web, cache, and extensions.
license: Apache-2.0
---

# ddd4j-boot Architecture

## Overview

Targets the current ddd4j-boot maintenance line: parent, dependencies, bom, core, auth, data, mq, web, cache, extensions, samples. Confirm the version line first, then apply this skill.

## Core Scope

parent, dependencies, bom, core, auth, data, mq, web, cache, extensions, samples.

## Rules

1. The Boot layer only assembles ddd4j capabilities; it does not copy core implementations.
2. Aggregator POMs stay separate from concrete implementation modules.
3. Conditional wiring and lifecycle belong to the concrete feature modules.
4. Each maintenance line keeps its own JDK/Maven/POM.
5. A module existing does not mean the auto-configuration has taken effect.

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

- "Use `$ddd4j-boot-architecture` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-boot-architecture` to review existing usage against the current source."
- "Use `$ddd4j-boot-architecture` to return an implementation choice, evidence state, and remaining risk."

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
