---
name: ddd4j-mq
description: Use when choosing, implementing, or reviewing ddd4j messaging with Kafka, RabbitMQ, Pulsar, RocketMQ, ActiveMQ, Artemis, MQTT, NATS, SQS, ONS, TDMQ, Redis Stream, Spring integration, acknowledgments, retries, dead letters, or lifecycle.
license: Apache-2.0
---

# ddd4j MQ

## Overview

All broker adapters unify onto MQClient, MQListener, MQEvent, and Acknowledgment; choose delivery and operational semantics first, then the broker.

## Broker Routing

| Requirement | Candidates |
|---|---|
| High-throughput logs/streams | Kafka |
| AMQP routing | RabbitMQ |
| Multi-tenant streams/queues | Pulsar/TDMQ |
| Domestic transactional/ordered messages | RocketMQ/ONS |
| JMS | ActiveMQ/Artemis |
| IoT | MQTT/Mica MQTT |
| Lightweight JetStream | NATS |
| AWS | SQS |
| Redis infrastructure | Redis Stream |
| In-process | Disruptor |
| Spring Cloud | unified by the Cloud Stream adapter |

## Core Rules

1. Required listeners that fail initialization must block startup; optional ones may degrade readiness.
2. Ack after successful business processing; on failure nack/requeue according to policy.
3. Retries need backoff, an upper bound, and dead-lettering.
4. Message id/business key drives idempotency; never rely on the broker alone.
5. Partial initialization failure must shut down already-created resources in reverse order.
6. close is idempotent; threads, consumers, producers, and connections all have owners.
7. Configurations such as persist=true must have behavior tests.

## Capability Boundaries

### ✅ Strong At

- Broker selection and the unified API.
- ACK/NACK, retries, dead letters, idempotency.
- Listener scanning and lifecycle.
- Testcontainers round-trips.

### ⚠️ Needs Input

- Broker, delivery semantics, and ordering requirements.
- topic/tag/group/namespace.
- Deployment and disaster-recovery model.

### ❌ Out of Scope

- Declaring the message chain successful because a container started.
- Using mocks to prove broker durability.
- Mechanically unifying topic naming across brokers.

## Workflow

1. Define at-most/at-least-once and ordering.
2. Choose the broker/adapter.
3. Configure producer/consumer/listener.
4. Verify publish→consume→ack.
5. Verify retry/dead-letter/duplicate/recovery.
6. Verify startup rollback, readiness, and shutdown.

## Common Mistakes

- ACK completed before business processing.
- Consumed failures being swallowed.
- A required consumer failing at startup while the app still reports READY.
- Counting a broker container start as a round-trip.
- Illegal characters in RocketMQ destinations.
- Writing skipped tests down as PASS.

## Deep Reference

- [Broker Matrix](references/broker-matrix.md)
- [ACK and Reliability](references/ack-retry-dead-letter.md)
- [Lifecycle](references/lifecycle.md)
- [Testing](references/testcontainers.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Message payloads, headers, and logs must not leak tokens, PII, or cloud access keys.

## Quick Start

- "Use `$ddd4j-mq` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-mq` to review existing usage against the current source."
- "Use `$ddd4j-mq` to return an implementation choice, evidence state, and remaining risk."

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
