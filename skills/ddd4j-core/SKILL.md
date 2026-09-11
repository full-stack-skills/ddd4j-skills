---
name: ddd4j-core
description: Use when implementing or reviewing current ddd4j domain models, aggregate roots, CQRS commands/queries, domain events, repository SPI, context, subject, cache, or health contracts; not for legacy io.hiwepy.boot CRUD conventions.
license: Apache-2.0
---

# ddd4j Core

## Overview

Guide domain modeling and framework-agnostic code against the current `io.ddd4j.core` public contracts. The core boundary is: `ddd4j-core` defines DDD / CQRS / SPI; Spring, Guice, Quarkus, Javalin, MyBatis, and friends only assemble in the adapter layer.

## Quick Start

- "Build an event-sourced aggregate with ddd4j."
- "Implement Command, CommandExecutor, and the CommandBus dispatch."
- "Review whether the domain layer wrongly depends on Spring or MyBatis."
- "Explain the boundary between `ThreadContext`, `Contexts`, and `Subject`."

## Audience, Routing, and Customization

- **Domain developers** — provide the aggregate strategy, target maintenance line, and business invariants.
- **Adapter developers** — provide the runtime, repository / bus implementation, and transaction boundaries.
- **Reviewers** — require read-only inspection and specify whether the focus is DDD, CQRS, context, or SPI.
- **Non-ddd4j projects** — hand off to the generic DDD / Java skills; do not retrofit ddd4j types.

When input is insufficient, give a tentative verdict based on the current checkout first, then list `missing: specific item; how to provide: path, branch, or contract`.

Always confirm the current branch first; the 1.0.x, 2.0.x, and 3.0.x APIs are not interchangeable by name.

## Capability Boundaries

### ✅ Strong At

1. `AggregateRoot<ID>` with both Active Record and Event Sourcing modes.
2. `Command`, `CommandExecutor`, `CommandBus`, and `Result<R>` write-side contracts.
3. `Query<M>`, `PersistenceQueryScope<M, P>`, and `Repository<M, ID>`.
4. `DomainEvent<ID>` metadata, publication, replay, and event handlers.
5. `Contexts` / `ThreadContext`, `Subject`, `Cache`, and other framework-agnostic SPIs.

### ⚠️ Needs Input

1. Target maintenance line with source code and POM.
2. Domain model, persistence strategy, and transaction boundary.
3. Runtime adapter and real acceptance behavior.

### ❌ Out of Scope

1. `io.hiwepy.boot.api.*` — `BaseEntity`, `PaginationEntity`, `ApiRestResponse`.
2. Treating Spring annotation semantics as the universal runtime contract.
3. Replacing specific MyBatis / JPA / Jackson / Sa-Token adapter skills.

## Core Rules

| Topic | Current Contract |
|---|---|
| Aggregate root | Extend `AggregateRoot<ID>`; the identifier implements `Serializable` |
| Persistence mode | Choose Active Record OR Event Sourcing — never mix both on the same aggregate |
| Events | Subclasses keep a no-arg constructor; use `registerEvent`, replay via `loadFromHistory` |
| Commands | `Command` expresses intent; executed by `CommandExecutor`, dispatched via `CommandBus.execute` |
| Queries | `Query<M>` binds to the domain model; opt into PO fields with explicit `persistence(P.class)` |
| Repository | Domain only depends on `Repository`; the implementation is registered by the data / runtime adapter |
| Context | Request / thread scopes must be released on completion — Subject or tenant data must not leak |
| Cache | Domain depends only on the `Cache` SPI; cross-instance atomic semantics must be proven by the implementation |

## Examples

```java
public final class Order extends AggregateRoot<OrderId> {
    private OrderStatus status;

    public void pay() {
        if (status == OrderStatus.PAID) {
            throw new IllegalStateException("Order already paid");
        }
        registerEvent(new OrderPaid(id()));
    }

    @EventHandler
    void apply(OrderPaid event) {
        status = OrderStatus.PAID;
    }
}
```

When using event sourcing, persist `pullDomainEvents()` and stop calling snapshot-style `save()` / `update()`.

## Workflow

1. Confirm the maintenance-line contract from current source and tests.
2. Decide whether the aggregate uses snapshot or event sourcing.
3. Keep Domain depending only on core APIs and SPIs.
4. Implement the repository, bus, and publisher in the data / runtime module.
5. Verify with aggregate invariants, event replay, command result, and context cleanup tests.

## Common Mistakes

- Continuing the legacy `BaseEntity / Model<T>` inheritance chain.
- Importing Spring or MyBatis Wrapper types directly into the core domain layer.
- Persisting both aggregate snapshots and uncommitted events.
- Treating `DomainEvent.source()` as a complete `EntityIdPath`.
- Assuming `Repository` default methods work without testing the actual adapter — they may throw `UnsupportedOperationException`.
- Binding `ThreadContext` but failing to clean it up in a `finally` block or scope close.

## Output and Exceptions

Cite specific package names, source paths, and maintenance lines. When a symbol cannot be resolved, return `missing: symbol or module in the current branch; how to provide: confirm branch, POM, and source path`. Do not substitute legacy project types.

## Capability Routing

- Module boundaries and dependency direction — hand off to **`ddd4j-architecture`**. Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-architecture`.
- Annotation semantics and consumers — hand off to **`ddd4j-annotation`**. Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-annotation`.
- Maven / BOM / version ownership — hand off to **`ddd4j-bom`**. Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-bom`.
- JSON, Bean, string, collection, and ID utilities — hand off to **`ddd4j-kit`**. Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-kit`.

## Privacy and Security

Examples use fictitious orders and identifiers. Never output real tokens, tenant data, user profiles, or private-repository credentials.

## FAQ

1. **Can I still use `BaseEntity`?** Only when an external project explicitly depends on it; it is not a current ddd4j-core contract.
2. **Must `AggregateRoot` use event sourcing?** No — but do not mix the two modes on the same aggregate.
3. **Can `Query` reference a PO?** Yes, via an explicit persistence scope. The domain `Query` itself binds to the aggregate root.
4. **Is `Repository` MyBatis-specific?** No — it is an ORM-agnostic SPI.
5. **Must `DomainService` be a Spring Bean?** Cannot be assumed across runtimes.
6. **What counts as proof of completion?** Current branch source, related tests, and verified runtime adapter behavior.

## Deep Reference

- [Source Evidence](references/source-evidence.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)
