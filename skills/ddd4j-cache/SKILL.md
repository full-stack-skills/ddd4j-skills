---
name: ddd4j-cache
description: Use when choosing, configuring, implementing, or reviewing ddd4j cache providers, local caches, Redis clients, JetCache, Memcached, TTL, locking, CAS, statistics, or cache-backed idempotency.
license: Apache-2.0
---

# ddd4j Cache

## Overview

Choose single-node or distributed consistency semantics first, then choose the implementation. All implementations are consumed by upper layers through the core Cache/CacheManager/CasCache/AtomicCache contracts.

## Implementation Selection

| Scenario | Implementation |
|---|---|
| Single-JVM high performance | Caffeine, Guava, Hutool |
| Native Redis clients | Lettuce, Jedis |
| Distributed locks/objects | Redisson |
| Multilevel/unified abstraction | JetCache |
| Memcached | MemcachedCache |

## Core Rules

1. Caffeine/Guava/Hutool provide no cross-instance consistency.
2. Cluster idempotency requires a shared atomic compare-and-set, not just distributed storage.
3. TTL units, zero values, negative values, and precision must be tested per implementation.
4. REDIS_OBJECT_MAPPER handles trusted cache data only.
5. Locks must have an owner, a timeout, and release on exception.
6. CacheStats cannot substitute for business success metrics.

## Capability Boundaries

### ✅ Strong At

- Implementation selection and configuration.
- TTL, locks, CAS, statistics.
- Local versus distributed semantics.
- Reviewing cache-backed idempotency.

### ⚠️ Needs Input

- Deployment instance count and consistency target.
- Cache keys/values, TTL, capacity.
- Redis/Memcached/JetCache runtime environment.

### ❌ Out of Scope

- Treating the cache as a database.
- Claiming a local Cache supports cluster idempotency.
- Flushing production caches without authorization.

## Workflow

1. Define data authority and invalidation policy.
2. Choose local/distributed/multilevel.
3. Verify get/put/invalidate, TTL, concurrency, and failure paths.
4. If idempotency is required, verify real CAS contention.
5. Add observability, capacity, and degradation strategy.

## Common Mistakes

- Still using Caffeine idempotency across multiple instances.
- Passing get-then-put off as CAS.
- Cache keys lacking tenant isolation.
- Deserializing untrusted cache content.
- Locks not released on exception paths.
- Silently returning success when Redis is unavailable.

## Deep Reference

- [Provider Matrix](references/provider-matrix.md)
- [CAS and Idempotency](references/cas-and-idempotency.md)
- [Serialization and Keys](references/serialization-and-keys.md)
- [Testing](references/testing.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Cache keys, values, and logs must not expose tokens, passwords, ID numbers, phone numbers, or tenant secrets.

## Quick Start

- "Use `$ddd4j-cache` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-cache` to review existing usage against the current source."
- "Use `$ddd4j-cache` to return an implementation choice, evidence state, and remaining risk."

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
