---
name: ddd4j-architecture
description: Use when designing, reviewing, or locating boundaries in ddd4j modules, DDD/CQRS layers, ports and adapters, runtime integrations, or dependency direction.
license: Apache-2.0
---

# ddd4j Architecture

## Overview

ddd4j's stable center is the framework-agnostic domain, CQRS, and SPI layer. The outer modules deliver data, messaging, web, authentication, caching, observability, and runtime adapters.

## Quick Start

- "Can the domain layer depend on a MyBatis Wrapper?"
- "Which module should assemble the CommandBus?"
- "Should a new broker live in core or in the mq module?"
- "How do Spring, Guice, and Quarkus CDI share the core contracts?"

## Architecture Zones

| Zone | Responsibility |
|---|---|
| annotation | DDD / CQRS / API / ORM metadata |
| core | AggregateRoot, Command/Query, Event, Repository, Context, SPI |
| kit | Foundational utilities, no business runtime |
| auth / data / mq / web / cache / metrics | Capability interfaces and their implementations |
| runtime-* | DI and lifecycle wiring for Spring, Guice, Quarkus, etc. |
| extensions | Cross-cutting optional extensions |
| ddd-rules | Architecture constraints and static checks |
| parent / dependencies / bom | Build, version ownership, and consumer surface |

## Decision Rules

1. Domain depends only on core, annotation, and necessary value types.
2. ORM, broker, HTTP, and authentication frameworks live in the adapter layer.
3. Static facades resolve implementations through Contexts, Registry, or SPI.
4. Framework runtimes own registration, request scoping, rollback, and shutdown.
5. BOM manages versions only — it does not prove runtime wiring succeeded.
6. The same aggregate must not mix snapshot Active Record with Event Sourcing.

## Capability Boundaries

### ✅ Strong At

- Module ownership and dependency direction.
- DDD / CQRS layering with ports and adapters.
- Sharing the core across multiple runtimes.
- Architecture review and landing new capabilities.

### ⚠️ Needs Input

- Target maintenance line and module POMs.
- Business behavior and transaction boundaries.
- Runtime and deployment model.

### ❌ Out of Scope

- Detailed framework API explanations.
- Concluding implementation from directory names alone.
- Unverified cross-line parity claims.

## Workflow

1. Confirm the Git root, branch, and CodeGraph health.
2. Trace core ports and their actual adapters from the call graph.
3. Mark compile dependencies, runtime registrations, and resource lifecycles.
4. Verify separately with architecture tests, behavior tests, and runtime evidence.
5. Report facts, inferences, violations, and proposed landing points.

## Common Mistakes

- Domain imports Spring, MyBatis, Javalin, or Quarkus types.
- Concrete broker or database clients created inside core.
- Missing runtime registration misdiagnosed as missing core API.
- Aggregate module names treated as functional evidence.
- Inspecting the dependency tree without reading calls and lifecycle.

## Output and Exceptions

Return `current branch, modules, ports, adapters, registration points, tests, risks`. When an implementation is missing, return `missing: specific adapter or registration point; how to provide: module or runtime` — never invent a fictitious chain.

## Deep Reference

- [Module Boundaries](references/module-boundaries.md)
- [Dependency Rules](references/dependency-rules.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Architecture evidence must not include credentials, real tenant data, or private Maven repository authentication.

## Audience and Customization

- Developers: provide the target modules, runtime, and behavior.
- Architects: specify a read-only boundary, migration, or compatibility review.
- Testers: specify the required evidence levels.

Customize the target maintenance line, allowed dependencies, and output depth. When input is insufficient, give a tentative verdict first, then list `missing: module or runtime; how to provide: POM and call site`.

## FAQ

1. **Are skills organized by module?** No — by decision domain.
2. **Does a directory's existence mean the capability is complete?** No.
3. **Can the domain layer depend on a framework?** It should not.
4. **What does the runtime layer do?** Registration and lifecycle.
5. **Does identical cross-line structure imply identical behavior?** No.
6. **What if an implementation is missing?** State the gap explicitly; do not invent one.
