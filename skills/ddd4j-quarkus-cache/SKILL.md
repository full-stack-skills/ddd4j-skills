---
name: ddd4j-quarkus-cache
description: Use when integrating Quarkus Cache, Redis, or ddd4j Cache SPI with Quarkus, including TTL, CAS, idempotency, bean scopes, and lifecycle.
license: Apache-2.0
---

# ddd4j-quarkus Cache

## Overview

Covers Quarkus Cache, Redis, the ddd4j Cache SPI, TTL, CAS, idempotency, and CDI scope uniformly, not split per artifact. Choose 3.3.x or 4.0.x first, then read the current source.

## Core Scope

Quarkus Cache, Redis, ddd4j Cache SPI, TTL, CAS, idempotency, CDI scope.

## Core Rules

1. 3.3.x and 4.0.x each keep their own ddd4j/JDK/Maven/POM/Quarkus contract.
2. 4.0.x is the adapter line name and does not mean Quarkus Platform 4.
3. CDI/Arc, runtime/deployment, and BuildItem/Recorder are not explained with the Spring model.
4. Bean scope, request Context, startup/shutdown, and native boundaries are explicit.
5. Report source, tests, CI, Security, and publishing in layers.

## Capability Boundaries

### ✅ Strong At

- Implementation choice for caching and Quarkus adaptation.
- CDI, build-time, and runtime boundaries.
- Differences between the two maintenance lines.

### ⚠️ Needs Input

- Target line, POM, and Quarkus Platform.
- Capabilities, runtime, and deployment requirements.
- Current source/test/CI evidence.

### ❌ Out of Scope

- Substituting the Spring assembly model for Quarkus.
- Treating a BOM import as a registered bean.
- Unauthorized releases or production changes.

## Workflow

1. Select the version line.
2. Locate runtime/deployment or feature modules.
3. Verify CDI scope, configuration, and lifecycle.
4. Read the appropriate Arc/QuarkusTest/contract evidence.
5. Output version, implementation, evidence, and risks.

## Output and Exceptions

When input is missing, output "missing: target line/extension/runtime; how to provide: supply the POM and acceptance behavior".

## Deep Reference

- [Feature Matrix](references/feature-matrix.md)
- [Source Evidence](references/source-evidence.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never output tokens, OIDC secrets, or database, broker, or private repository credentials.

## Quick Start

- "Use `$ddd4j-quarkus-cache` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-quarkus-cache` to review existing usage against the current source."
- "Use `$ddd4j-quarkus-cache` to return an implementation choice, evidence state, and remaining risk."

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
