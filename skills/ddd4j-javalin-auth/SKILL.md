---
name: ddd4j-javalin-auth
description: Use when integrating Sa-Token, Apache Shiro, or OIDC and Keycloak authentication with ddd4j-javalin routes, Subject providers, authorization, errors, and request cleanup.
license: Apache-2.0
---

# ddd4j-javalin Auth

## Overview

Covers Sa-Token, Shiro, OIDC/Keycloak, SubjectProvider, route protection, 401/403, and cleanup uniformly. Confirm the maintenance line with ddd4j-javalin-version-selection first, then read the current branch source.

## Core Scope

Sa-Token, Shiro, OIDC/Keycloak, SubjectProvider, route protection, 401/403, cleanup.

## Core Rules

1. 6.7.x, 7.1.x, and 7.2.x each keep their own Javalin/JDK/Maven/POM contract.
2. Javalin 6 versus 7 API differences are aligned by behavior, not copied mechanically.
3. Report configuration, startup, HTTP, containers, CI, and publishing in layers.
4. Context/Subject/resources are cleaned on success, exception, and async terminal states.
5. Production dependencies need real readiness, shared CAS, explicit CORS, and idempotent close.

## Capability Boundaries

### ✅ Strong At

- Implementation choice for authentication and Javalin adaptation.
- Lifecycle, configuration, and behavior boundaries.
- Differences across the three maintenance lines.

### ⚠️ Needs Input

- Target branch, POM, and Javalin version.
- Business behavior, dependencies, and deployment mode.
- Current source/test/CI evidence.

### ❌ Out of Scope

- Copying Javalin 6 code directly to 7.
- Substituting smoke tests for real behavior.
- Unauthorized releases or production changes.

## Workflow

1. Select the version line.
2. Locate feature modules, entry points, and providers.
3. Compare implementations, configuration, overrides, and degradation.
4. Read/execute the appropriate contract evidence.
5. Output version, behavior, lifecycle, and risks.

## Output and Exceptions

When input is missing, output "missing: target line/implementation/configuration; how to provide: supply the POM and acceptance behavior", and continue safe read-only checks.

## Deep Reference

- [Feature Matrix](references/feature-matrix.md)
- [Source Evidence](references/source-evidence.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never output tokens, cookies, OIDC secrets, or database or private repository credentials.

## Quick Start

- "Use `$ddd4j-javalin-auth` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-javalin-auth` to review existing usage against the current source."
- "Use `$ddd4j-javalin-auth` to return an implementation choice, evidence state, and remaining risk."

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
