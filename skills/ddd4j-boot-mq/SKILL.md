---
name: ddd4j-boot-mq
description: Use when integrating ddd4j MQ adapters in Spring Boot, including broker auto-configuration, listener scanning, required or optional consumers, acknowledgment, retry, dead letter, readiness, and shutdown.
license: Apache-2.0
---

# ddd4j-boot MQ

## Overview

Covers Kafka, RabbitMQ, Pulsar, RocketMQ, ActiveMQ, MQTT, NATS, SQS, ONS/TDMQ, and listener lifecycle uniformly, not split per artifact. Before use, confirm the maintenance line through ddd4j-boot-version-selection.

## Core Scope

Kafka, RabbitMQ, Pulsar, RocketMQ, ActiveMQ, MQTT, NATS, SQS, ONS/TDMQ, listener lifecycle.

## Core Rules

1. Gather evidence from the current target line's POMs, source, and tests.
2. Default implementations allow explicit user overrides; an off switch must truly skip assembly.
3. Report configuration presence, bean creation, behavior tests, CI, and publishing separately.
4. Resources must have an explicit owner, failure rollback, and idempotent close.
5. Handle Boot 2/3/4 API, JDK, and Maven differences line by line.

## Capability Boundaries

### ✅ Strong At

- Choosing among MQ implementations and Spring Boot assembly.
- Configuration, overrides, lifecycle, and verification.
- Maintenance-line compatibility judgments.

### ⚠️ Needs Input

- Target Boot line, POM, and configuration.
- Business behavior, dependencies, and deployment mode.
- Current test/CI/runtime evidence.

### ❌ Out of Scope

- Modifying ddd4j core public semantics.
- Substituting dependency or bean presence for real behavior.
- Unauthorized releases or production operations.

## Workflow

1. Select the version line.
2. Locate the feature's aggregator and concrete implementations.
3. Compare implementations, defaults, overrides, and degradation.
4. Execute target context and behavior tests.
5. Output version, configuration, lifecycle, evidence, and risks.

## Output and Exceptions

When information is missing, output "missing: target line/implementation/configuration; how to provide: supply the POM and acceptance behavior", and continue safe read-only checks.

## Deep Reference

- [Feature Matrix](references/feature-matrix.md)
- [Source Evidence](references/source-evidence.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never output credentials, tokens, production connection strings, or sensitive business data.

## Quick Start

- "Use `$ddd4j-boot-mq` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-boot-mq` to review existing usage against the current source."
- "Use `$ddd4j-boot-mq` to return an implementation choice, evidence state, and remaining risk."

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
