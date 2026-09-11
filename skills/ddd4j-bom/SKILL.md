---
name: ddd4j-bom
description: Use when choosing or changing ddd4j parent, dependencies, BOM imports, Maven model, version ownership, dependency properties, release-line alignment, or consumer dependency management.
license: Apache-2.0
---

# ddd4j BOM and Maven Governance

## Overview

`parent` owns the build, `dependencies` owns third-party versions, `BOM` owns ddd4j consumer coordinates. The three have distinct responsibilities. Adapter-project BOMs own only their own ecosystem versions.

## Quick Selection

| Need | Use |
|---|---|
| Plugin, compile, and publish defaults | `ddd4j-parent` |
| Third-party `dependencyManagement` | `ddd4j-dependencies` |
| Business consumer imports ddd4j module versions | `ddd4j-bom` |
| Boot / Javalin / Quarkus / Cloud specific versions | Corresponding adapter-project `dependencies` / BOM |

## Core Rules

1. `1.0.x` / `2.0.x` stay on POM 4.0 / Maven 3. `3.0.x` uses POM 4.1 / Maven 4.
2. POM 4.0 uses `<modules>` / `<module>`. POM 4.1 uses `<subprojects>` / `<subproject>`.
3. Concrete modules must not duplicate third-party versions already managed by `dependencies`.
4. `ddd4j-dependencies` is the authoritative platform dependency source.
5. Boot / Cloud / Javalin / Quarkus BOMs manage only their own ecosystem surface.
6. BOM import order affects the effective version — always check the effective POM.
7. A resolvable parent / BOM does not mean every JAR is published.

## Capability Boundaries

### ✅ Strong At

- Choosing between `parent`, `dependencies`, and BOM responsibilities.
- Maven 3 / 4 and Model 4.0 / 4.1 differences.
- Property layout, version leakage, and import conflicts.
- Aligning dependencies across multiple maintenance lines and verifying consumption.

### ⚠️ Needs Input

- Current maintenance line and JDK / Maven versions.
- Target POM and effective POM.
- Private / central Maven resolution results.

### ❌ Out of Scope

- Silently changing versions or publishing.
- Using `enforcer.skip` as proof of release.
- Inferring ownership from XML keywords alone.

## Validation Gates

- `scripts/test_maven4_model_contract.py`
- `scripts/test_dependency_property_layout.py`
- `scripts/test_bom_import_conflicts.py`
- `scripts/test_dependency_alignment.py`
- `scripts/check-bom-alignment.sh`
- Clean-cache consumer `dependency:go-offline` / `compile`

## Common Mistakes

- Mixing BOM and parent responsibilities.
- Scattered numeric versions inside concrete modules.
- Keeping `<modules>` in Maven 4 aggregator POMs.
- Reading the source POM without checking the effective POM.
- Claiming a full release after only some modules uploaded.
- A warm private-repository cache masking missing parent / BOM artifacts.

## Output and Exceptions

Return `maintenance line, JDK, Maven, POM Model, version owners, effective POM, and consumption state`. When missing, return `missing: effective model or remote coordinate; how to provide: run help:effective-pom or a clean-cache resolve`.

## Deep Reference

- [Ownership and Imports](references/ownership-and-imports.md)
- [Maven Model](references/maven-model.md)
- [Publication and Consumption](references/publication-and-consumption.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never print `settings.xml`, server passwords, or private-repository tokens.

## Quick Start

- "Use `$ddd4j-bom` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-bom` to review existing usage against the current source."
- "Use `$ddd4j-bom` to return an implementation choice, evidence state, and remaining risk."

## Audience and Customization

- Developers: provide the target maintenance line, POM, capabilities, and acceptance behavior.
- Architects: specify a read-only boundary, compatibility, or migration review.
- Testers / release engineers: specify the required evidence levels; do not auto-expand to release or production operations.

Customize the target framework, allowed implementations, excluded modules, compatibility requirements, and evidence level. When input is insufficient, give a tentative verdict first, then list `missing: specific item; how to provide: path or configuration`.

## FAQ

1. **Are skills organized by Maven artifact?** No — by the user-facing capability domain.
2. **Can I copy another maintenance line directly?** No — verify the version and source first.
3. **Does a class existing in source prove the capability works?** No — registration and behavior evidence are also required.
4. **How do I report tests that did not run?** Mark `NOT RUN` or `BLOCKED`.
5. **Can the skill commit or release automatically?** Only after explicit user authorization.
6. **What if the implementation is missing?** Describe the missing module or evidence; do not invent APIs.
