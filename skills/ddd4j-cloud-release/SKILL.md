---
name: ddd4j-cloud-release
description: Use when validating, publishing, or remotely consuming all ddd4j-cloud maintenance lines, including upstream Boot and ddd4j artifacts, Maven 3 or 4, private repository recovery, and clean-cache proof.
license: Apache-2.0
---

# ddd4j-cloud Release

## Overview

Covers the eight-line serial build, upstream Boot/ddd4j, Maven 3/4, private repository recovery, remote metadata, and clean-cache consumption uniformly, not split per artifact. Choose the Cloud→Boot→ddd4j primary combination first, then read the current branch.

## Core Scope

Eight-line serial build, upstream Boot/ddd4j, Maven 3/4, private repository recovery, remote metadata, clean-cache consumption.

## Core Rules

1. Primary combinations and compatible alternatives are kept separate; never guess Boot/ddd4j from the branch name.
2. Old cmpt and new extensions naming must not be mixed.
3. Context/Tenant are restored on sync, async, Reactor, and Feign terminal states.
4. Binder, database, Nacos, Sentinel, and the like need real external behavior evidence.
5. Upstream gaps, Cloud failures, CI, publishing, and consumption are classified separately.

## Capability Boundaries

### ✅ Strong At

- Implementation choice for release work and Spring Cloud integration.
- Upstream/downstream versions and cross-service boundaries.
- Differences across the eight maintenance lines.

### ⚠️ Needs Input

- Target Cloud line, Boot parent, and POM.
- Capabilities, external services, and deployment requirements.
- Current source/test/remote evidence.

### ❌ Out of Scope

- Treating README module names as completed capabilities.
- Substituting configuration presence for external service behavior.
- Unauthorized releases or production operations.

## Workflow

1. Select the primary version combination.
2. Locate extensions, entry points, and upstream/downstream dependencies.
3. Compare implementations, propagation, degradation, and lifecycle.
4. Read the appropriate contract/verified-consumer evidence.
5. Output version, implementation, external dependencies, and risks.

## Output and Exceptions

When input is missing, output "missing: Cloud line/upstream/external services; how to provide: supply the POM and acceptance behavior".

## Deep Reference

- [Feature Matrix](references/feature-matrix.md)
- [Source Evidence](references/source-evidence.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never output Nacos/Redis/broker/database/private repository credentials or real tenant data.

## Quick Start

- "Use `$ddd4j-cloud-release` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-cloud-release` to review existing usage against the current source."
- "Use `$ddd4j-cloud-release` to return an implementation choice, evidence state, and remaining risk."

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
