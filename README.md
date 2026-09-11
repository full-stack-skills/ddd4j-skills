<div align="center">

# ddd4j-skills

**Source-aligned Agent Skills for ddd4j maintenance and production delivery**

[简体中文](./README.zh-CN.md)

</div>

## Overview

This package separates ddd4j-specific contracts from generic Java guidance and general DDD methodology. Every skill must be verified against the target maintenance line's source, POMs, tests, and runtime evidence.

## Install

```bash
npx skills add full-stack-skills/ddd4j-skills
```

Install one skill:

```bash
npx skills add full-stack-skills/ddd4j-skills --skill <skill-name>
```

## Skills (15)

| Skill | Use when |
|---|---|
| `ddd4j-version-selection` | Selecting compatible ddd4j, Boot, Cloud, Javalin, Quarkus, JDK, Maven, and POM versions |
| `ddd4j-architecture` | Designing and reviewing ddd4j module boundaries, DDD/CQRS layers, ports, adapters, and runtimes |
| `ddd4j-annotation` | Selecting and reviewing ddd4j DDD, CQRS, API, and ORM annotations and their consumers |
| `ddd4j-bom` | Governing ddd4j parent, dependencies, BOM imports, Maven models, and version ownership |
| `ddd4j-core` | Working with AggregateRoot, CQRS, DomainEvent, Repository, Context, Subject, or Cache contracts |
| `ddd4j-kit` | Selecting ddd4j JSON, bean, string, collection, identifier, function, and reflection utilities |
| `ddd4j-data` | Choosing JDBC, JDBI, JPA, MyBatis, R2DBC, Panache, EventStore, Projection, Outbox, and transactions |
| `ddd4j-web` | Applying common HTTP, context, error, validation, auth, idempotency, CORS, and readiness contracts across runtimes |
| `ddd4j-auth` | Choosing and integrating Sa-Token, Shiro, or Spring Security through ddd4j Subject contracts |
| `ddd4j-cache` | Choosing local, Redis, Redisson, JetCache, Memcached, TTL, locking, and CAS behavior |
| `ddd4j-mq` | Choosing and operating Kafka, RabbitMQ, Pulsar, RocketMQ, MQTT, NATS, SQS, acknowledgments, and lifecycle |
| `ddd4j-metrics` | Instrumenting projection, Web, MQ, cache, runtime, and OpenTelemetry metrics |
| `ddd4j-runtime` | Integrating Spring, Guice, Quarkus CDI, Micronaut, Vert.x, Helidon, and Dropwizard runtimes |
| `ddd4j-extensions` | Choosing optional Excel, license, monitor, OpenTelemetry, PF4J, QLExpress, QR code, and validation extensions |
| `ddd4j-javalin-production-hardening` | Hardening and releasing ddd4j-javalin across its maintenance branches |

## Boundaries

- Use `java-skills` for generic Java libraries and conventions.
- Use `ddd-skills` for general DDD architecture and modeling.
- Use this package for ddd4j source contracts, adapters, maintenance lines, and release gates.

## License

Apache-2.0. See [LICENSE](LICENSE).
