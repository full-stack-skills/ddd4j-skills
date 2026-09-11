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

## Skills (50)

| Skill | Use when |
|---|---|
| `ddd4j-version-selection` | Selecting compatible ddd4j, Boot, Cloud, Javalin, Quarkus, JDK, Maven, and POM versions |
| `ddd4j-boot-version-selection` | Selecting one of the 13 ddd4j-boot maintenance lines for a Spring Boot/JDK/Maven baseline |
| `ddd4j-boot-architecture` | Designing ddd4j-boot module boundaries and Spring Boot integration responsibilities |
| `ddd4j-boot-bom` | Managing ddd4j-boot parent, dependencies, BOM, effective POM, and version ownership |
| `ddd4j-boot-autoconfiguration` | Building conditional auto-configurations, properties, user overrides, imports, and lifecycle |
| `ddd4j-boot-auth` | Integrating Sa-Token, Shiro, and Spring Security in ddd4j-boot |
| `ddd4j-boot-data` | Integrating JDBC, JPA, MyBatis, migrations, transactions, projections, and Outbox |
| `ddd4j-boot-cache` | Configuring local, Redis, Redisson, JetCache, TTL, CAS, and idempotency caches |
| `ddd4j-boot-mq` | Configuring multi-broker MQ, listeners, acknowledgment, retry, readiness, and shutdown |
| `ddd4j-boot-web` | Building MVC/WebFlux context, errors, auth, validation, idempotency, CORS, and readiness |
| `ddd4j-boot-observability` | Configuring Actuator, health, metrics, tracing, logging, monitoring, and OpenTelemetry |
| `ddd4j-boot-extensions` | Integrating Akka, Excel, QLExpress, QR code, monitor, and other optional extensions |
| `ddd4j-boot-testing` | Testing auto-configurations, maintenance matrices, HTTP, databases, Redis, and brokers |
| `ddd4j-boot-release` | Validating and publishing 13 maintenance lines with CI and clean-cache consumption |
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
| `ddd4j-javalin-version-selection` | Selecting the 6.7.x, 7.1.x, or 7.2.x Javalin maintenance line |
| `ddd4j-javalin-architecture` | Designing Javalin module and integration boundaries |
| `ddd4j-javalin-runtime` | Managing startup, SPI, readiness, drain, rollback, hooks, and close |
| `ddd4j-javalin-auth` | Integrating Sa-Token, Shiro, or OIDC/Keycloak |
| `ddd4j-javalin-data` | Integrating MyBatis, JPA/PostgreSQL, repositories, transactions, EventStore, and Outbox |
| `ddd4j-javalin-web` | Building routes, context, errors, CORS, auth, validation, idempotency, and health |
| `ddd4j-javalin-mq` | Wiring MQ listeners, acknowledgment, retry, readiness, and shutdown |
| `ddd4j-javalin-cache` | Selecting local or distributed cache, CAS, TTL, and idempotency backends |
| `ddd4j-javalin-extensions` | Composing Guice modules, business overrides, and extension lifecycle |
| `ddd4j-javalin-testing` | Testing HTTP, Keycloak, PostgreSQL, MQ, Docker, ports, and lifecycle |
| `ddd4j-javalin-release` | Validating and publishing all three maintenance lines |
| `ddd4j-quarkus-version-selection` | Selecting the 3.3.x or 4.0.x adapter line and compatible Quarkus Platform |
| `ddd4j-quarkus-architecture` | Designing Quarkus parent, BOM, extension, auth, data, MQ, Web, and cache boundaries |
| `ddd4j-quarkus-extension-authoring` | Building runtime/deployment modules, processors, BuildItems, recorders, and native support |
| `ddd4j-quarkus-runtime` | Integrating CDI/Arc, buses, publishers, Subject providers, context, startup, and shutdown |
| `ddd4j-quarkus-auth` | Integrating JWT, OIDC, Shiro, and Sa-Token support boundaries |
| `ddd4j-quarkus-data` | Integrating Panache, JPA, JDBI, R2DBC, tenants, transactions, EventStore, and Outbox |
| `ddd4j-quarkus-web` | Building Quarkus REST context, errors, auth, validation, idempotency, CORS, and readiness |
| `ddd4j-quarkus-mq` | Integrating Kafka, NATS, other brokers, acknowledgment, lifecycle, and containers |
| `ddd4j-quarkus-cache` | Integrating Quarkus Cache, Redis, ddd4j Cache SPI, TTL, CAS, and idempotency |
| `ddd4j-quarkus-testing` | Testing QuarkusTest, TestResource, Arc, Docker, classloaders, and native paths |
| `ddd4j-quarkus-release` | Validating and publishing 3.3.x/4.0.x with CI, Security, and clean-cache consumption |

## Boundaries

- Use `java-skills` for generic Java libraries and conventions.
- Use `ddd-skills` for general DDD architecture and modeling.
- Use this package for ddd4j source contracts, adapters, maintenance lines, and release gates.

## License

Apache-2.0. See [LICENSE](LICENSE).
