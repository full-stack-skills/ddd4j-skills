---
name: ddd4j-runtime
description: Use when integrating or reviewing ddd4j runtime bindings for Spring, Guice, Quarkus CDI, Micronaut, Vert.x, Helidon, or Dropwizard, including SPI registration, context, buses, publishers, readiness, startup rollback, and shutdown.
license: Apache-2.0
---

# ddd4j Runtime

## Overview

The runtime binds framework containers to the ddd4j core ports; core does not depend on any DI framework, and the runtime owns unique registration, request scope, and resource lifecycle.

## Runtimes

Spring, Guice, Quarkus CDI, Micronaut, Vert.x, Helidon, Dropwizard, plus runtime-testkit.

## Unified Responsibilities

- Register SPIs such as CommandBus, DomainEventPublisher, SubjectProvider, and Cache/Repository.
- Establish Request/Thread/Reactive Context.
- Initialize dependencies and aggregate readiness.
- Roll back in reverse order on partial failure.
- Idempotent close after drain.
- Prevent duplicate registration and shutdown hook leaks.

## Capability Boundaries

### ✅ Strong At

- DI/SPI assembly.
- Context and Subject lifecycle.
- Startup/readiness/drain/close.
- Behavior alignment across runtimes.

### ⚠️ Needs Input

- Target runtime and maintenance line.
- The SPIs that need registration.
- Resource dependencies and shutdown order.

### ❌ Out of Scope

- Applying Spring annotations to every runtime.
- Arbitrary overrides after duplicate registration.
- Declaring the runtime ready because a container started.

## Workflow

1. List the ports and providers.
2. Define the dependency order.
3. Register and detect duplicates.
4. Bind/restore the request context.
5. Aggregate readiness.
6. Roll back in reverse order, drain, close.
7. Test with runtime-testkit and the target framework.

## Deep Reference

- [Runtime Matrix](references/runtime-matrix.md)
- [SPI Registration](references/spi-registration.md)
- [Lifecycle](references/lifecycle.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

The Context must not leak Subject, Tenant, or Token across requests.

## Quick Start

- "Use `$ddd4j-runtime` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-runtime` to review existing usage against the current source."
- "Use `$ddd4j-runtime` to return an implementation choice, evidence state, and remaining risk."

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
