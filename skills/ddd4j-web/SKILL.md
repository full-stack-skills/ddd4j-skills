---
name: ddd4j-web
description: Use when implementing or reviewing ddd4j HTTP contracts across Spring MVC, WebFlux, Javalin, Quarkus REST, Micronaut, Vert.x, Helidon, or Dropwizard, including context, errors, validation, authentication, idempotency, CORS, limits, and readiness.
license: Apache-2.0
---

# ddd4j Web

## Overview

`ddd4j-web-core` defines the cross-runtime behavior. Each adapter implements the same HTTP contract. Framework APIs may differ, but response, context, and security behavior must remain consistent.

## Runtimes and Capabilities

Spring MVC, WebFlux, Javalin, Quarkus REST, Micronaut, Vert.x, Helidon, Dropwizard — uniformly covering response / errors, Request / Trace / Tenant context, authentication, idempotency, CORS, request size, async timeout, liveness / readiness, and validation.

## Core Rules

1. Bind context at request start; clean up on success, exception, and async completion.
2. Authentication failures, authorization failures, validation failures, and system errors use stable status codes and payloads.
3. Idempotency distinguishes closed, single-instance, and shared CAS scopes.
4. CORS in production uses an explicit allowlist.
5. Liveness and readiness are separate; readiness aggregates real dependencies.
6. The Testkit contract is the cross-runtime alignment evidence.

## Capability Boundaries

### ✅ Strong At

- A unified contract across multiple web runtimes.
- Context, errors, authentication, idempotency, CORS, and readiness.
- The four ddd4j validation constraints.
- HTTP contract testing.

### ⚠️ Needs Input

- Target runtime and maintenance line.
- Public endpoints and error contract.
- Deployment, proxy, and authentication mode.

### ❌ Out of Scope

- Treating HTTP 200 as proof of business correctness.
- Hardcoding `READY`.
- Leaking framework Context into the domain layer.

## Workflow

1. Choose the runtime and read the matching adapter.
2. Define the behavior with the web-testkit paths and payloads.
3. Implement binding, authentication, handling, exceptions, and cleanup.
4. Configure CORS, limits, idempotency, and readiness.
5. Run normal, error, replay, and same-thread reuse tests.

## Deep Reference

- [Runtime Matrix](references/runtime-matrix.md)
- [Context and Errors](references/context-and-errors.md)
- [Validation](references/validation.md)
- [Idempotency, CORS, Readiness](references/production-controls.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never log `Authorization`, `Cookie`, full request bodies, or private fields.

## Quick Start

- "Use `$ddd4j-web` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-web` to review existing usage against the current source."
- "Use `$ddd4j-web` to return an implementation choice, evidence state, and remaining risk."

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
