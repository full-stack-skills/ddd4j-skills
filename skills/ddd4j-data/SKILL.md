---
name: ddd4j-data
description: Use when choosing, implementing, or reviewing ddd4j persistence with JDBC, JDBI, JPA, MyBatis, MyBatis-Plus, R2DBC, Panache, EventStore, Projection, Outbox, transactions, tenants, or Domain-to-PO mapping.
license: Apache-2.0
---

# ddd4j Data

## Overview

Pick the persistence model first, then the technology. Snapshot Repository, Event Sourcing, Projection, and Outbox are distinct responsibilities that may be combined but must not blur transaction boundaries.

## Technology Selection

| Capability | Implementation |
|---|---|
| Synchronous SQL | JDBC, JDBI |
| ORM | JPA |
| Mapper | MyBatis, MyBatis-Plus |
| Reactive | R2DBC |
| Quarkus ORM | Panache |
| Event storage | JDBI / JPA / R2DBC / Panache / ESDB EventStore |
| Read model | Projection + multi-runtime scheduler / repository |
| Reliable publish | Transactional Outbox |

## Core Rules

1. Keep Domain `AggregateRoot` separate from PO / Entity.
2. The `Repository` port lives in core; the implementation lives in data.
3. `Query` binds to the domain model; PO fields are mapped through a persistence scope or metadata.
4. EventStore append must validate the expected version and batch atomicity.
5. Projection position updates and read-model writes need an explicit transaction and idempotency.
6. The Outbox must share a transaction with the business write, then claim / send / confirm independently.
7. Real-database tests prove dialect, transaction, concurrency, and visibility behavior.

## Capability Boundaries

### ✅ Strong At

- Technology selection and Domain / PO mapping.
- Repository, EventStore, Projection, Outbox.
- Tenant, data scope, and encrypted fields.
- Synchronous and reactive transaction boundaries.

### ⚠️ Needs Input

- Database, runtime, and maintenance line.
- Aggregate, PO, Query, and ID.
- Consistency and concurrency requirements.

### ❌ Out of Scope

- Treating an H2 unit test as production database proof.
- Defaulting to in-memory filtering on production-sized data.
- Using focused tests to claim transaction or concurrency coverage.

## Workflow

1. Choose snapshot or event sourcing.
2. Define the Aggregate / PO / Query mapping.
3. Choose JDBC, JDBI, JPA, MyBatis, R2DBC, or Panache.
4. Define transactions, tenants, encryption, and auditing.
5. When read models or publishing are needed, add Projection or Outbox.
6. Run real-database, rollback, concurrency, and recovery tests.

## Common Mistakes

- `AggregateRoot` becoming the framework PO directly.
- Raw MyBatis in-memory filtering going to production.
- EventStore and business writes committing separately.
- `MAX(position)+1` allocating global positions under concurrency.
- Projection advancing the cursor before writing the read model.
- Outbox marked as sent but unconfirmed / sent again without idempotency.

## Deep Reference

- [Storage Selection](references/storage-selection.md)
- [MyBatis](references/mybatis.md)
- [EventStore](references/event-store.md)
- [Projection](references/projection.md)
- [Outbox and Transactions](references/outbox-and-transactions.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Test data must be masked. SQL, event, and Outbox logs must not expose credentials or private payloads.

## Quick Start

- "Use `$ddd4j-data` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-data` to review existing usage against the current source."
- "Use `$ddd4j-data` to return an implementation choice, evidence state, and remaining risk."

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
