---
name: ddd4j-metrics
description: Use when instrumenting or reviewing ddd4j projection, runtime, Web, MQ, cache, or domain-operation metrics, especially OpenTelemetry counters, timers, failures, labels, and observability evidence.
license: Apache-2.0
---

# ddd4j Metrics

## Overview

Metrics must describe observable behavior and keep cardinality low; the current first-party implementation centers on ProjectionMetrics and OpenTelemetryProjectionMetrics, with other capabilities extended per real adapter.

## Core Rules

1. Ports are defined in the core capability; OpenTelemetry lives in the metrics/extension adapter.
2. success/failure, duration, and processed count are kept separate.
3. tenant/user/message id are not high-cardinality labels.
4. A Noop implementation is a degradation, not observability success.
5. Metric tests verify names, labels, increments, and exception paths.
6. Metrics cannot substitute for logs, traces, readiness, or business acceptance.

## Capability Boundaries

### ✅ Strong At

- ProjectionMetrics/OpenTelemetry.
- Web/MQ/Cache/Runtime metric design.
- Label cardinality and privacy review.
- Metric testing and evidence grading.

### ⚠️ Needs Input

- Observability backend and naming convention.
- SLI/SLO and alerting targets.
- Current instrumentation in the target modules.

### ❌ Out of Scope

- Inventing metrics that do not exist.
- PII as labels.
- Claiming production observability because metrics exist.

## Deep Reference

- [Projection Metrics](references/projection.md)
- [Cross-Capability Metrics](references/cross-capability.md)
- [Testing and Alerting](references/testing-and-alerting.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Labels must not contain tokens, user IDs, phone numbers, full URLs, SQL, or message bodies.

## Quick Start

- "Use `$ddd4j-metrics` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-metrics` to review existing usage against the current source."
- "Use `$ddd4j-metrics` to return an implementation choice, evidence state, and remaining risk."

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
