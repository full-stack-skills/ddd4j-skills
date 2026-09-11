---
name: ddd4j-annotation
description: Use when selecting, applying, reviewing, or extending current ddd4j annotations for DDD metadata, CQRS events, API behavior, ORM mapping, idempotency, auditing, or tenant fields.
license: Apache-2.0
---

# ddd4j Annotation

## Overview

Choose annotations by their consumers and runtime semantics. Do not assume that an annotation's name implies it registers a Bean, persists a field, or fires an event.

## Quick Routing

| Need | Family |
|---|---|
| Domain classification and metadata | ddd, Contract, BusinessType |
| Create / Update / Delete events | cqrs |
| Idempotency, module, operation log, raw response | api |
| Domain / PO mapping, tenant, audit, ordering | orm |

## Usage Rules

1. Inspect Retention, Target, defaults, and consumers before applying.
2. `RUNTIME` retention only means the annotation is reflectively visible; it does not mean the framework auto-handles it.
3. ORM annotations are consumed by `DomainModelHelper`, repositories, or interceptors.
4. API annotations must have their behavior implemented by a Web / Runtime adapter.
5. New annotations must ship with independence, default-value, target, and consumer tests.
6. Verify package names and Java / Jakarta differences across maintenance lines.

## Capability Boundaries

### ✅ Strong At

- `Contract`, `BusinessType`, `DDDAnnotation`.
- `ApiIdempotent`, `ApiModule`, `ApiOperationLog`, `RawResponse`.
- `CreateEvent`, `UpdateEvent`, `DeleteEvent`.
- `DomainField`, `TenantId`, `SystemId`, `BizKey`, `OnCreate`, `OnUpdate`, `OrderBy`.

### ⚠️ Needs Input

- Current maintenance line.
- Annotation target element and intended consumer.
- Web, Data, or Runtime adapter availability.

### ❌ Out of Scope

- Claiming a feature works because an annotation is present.
- Treating Spring or Quarkus annotations as ddd4j annotations.
- Changing retention or target without compatibility review.

## Examples

```java
public final class OrderPO {
    @BizKey
    private String orderNo;

    @TenantId
    private String tenantId;

    @OnCreate
    private Instant createdAt;

    @OnUpdate
    private Instant updatedAt;
}
```

The example expresses metadata only. Whether the fields are populated and isolated depends on the Data adapter.

## Common Mistakes

- Treating `DDDAnnotation` as `@Component`.
- Using `@ApiIdempotent` without an `IdempotencyGuard` wired in.
- Letting Domain reference PO after a `@DomainField` mapping is configured.
- `@TenantId` field present but no tenant bound in the request context.
- `@OnCreate` / `@OnUpdate` without an interceptor or repository backing them.
- CQRS event annotations without a corresponding publish test.

## Output and Exceptions

Return `annotation FQN, retention, target, attributes, consumers, validation tests`. When a consumer is missing, return `missing: runtime handler; how to provide: confirm target Web/Data/Runtime module`.

## Deep Reference

- [DDD and Contract](references/ddd-and-contract.md)
- [API and CQRS](references/api-and-cqrs.md)
- [ORM](references/orm.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Log, tenant, and authentication-related annotations must not cause sensitive fields or full request bodies to leak.

## Quick Start

- "Use `$ddd4j-annotation` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-annotation` to review existing usage against the current source."
- "Use `$ddd4j-annotation` to return an implementation choice, evidence state, and remaining risk."

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
