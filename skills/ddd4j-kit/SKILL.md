---
name: ddd4j-kit
description: Use when selecting or applying current ddd4j utility APIs for JSON, bean mapping, strings, collections, identifiers, functions, dates, arrays, reflection, or low-level reusable helpers.
license: Apache-2.0
---

# ddd4j Kit

## Overview

Prefer the stable utilities already shipped by ddd4j. Avoid duplicating them in business modules. Always confirm a tool's null handling, exception contract, type semantics, and thread safety before adopting it.

## Routing

| Need | Utility family |
|---|---|
| JSON / Jackson, type conversion | `JsonKit` |
| Bean properties and mapping | `BeanKit`, `MappingKit` |
| Strings | `StrKit`, `StrPool` |
| Collections and arrays | `CollKit`, `ArrayKit` |
| Identifiers | `IdKit` |
| Functions and type conversion | `FunctionKit` |
| Dates and times | `DateKit` and related formatters |
| Reflection | `ReflectKit` and explicit metadata tools |

## JSON Boundaries

- 3.0.x `JsonKit` uses `tools.jackson` databind.
- `DEFAULT_OBJECT_MAPPER` is for ordinary JSON.
- `REDIS_OBJECT_MAPPER` enables `DefaultTyping` and only handles trusted cache data.
- `EventStore` uses `EventPayloadSerializer` with explicit event types — never the Redis mapper.
- `com.fasterxml.jackson.annotation` exists as a Jackson 2 / 3 compatibility annotation package.

## Capability Boundaries

### ✅ Strong At

- Tool selection, null handling, and exception semantics.
- Boundary between `JsonKit` and Jackson 2 / 3.
- Common Bean, collection, string, and ID operations.
- Avoiding duplicate utility wrappers.

### ⚠️ Needs Input

- Current maintenance line.
- Input types and desired exception strategy.
- JSON usage scenario — HTTP, cache, or events.

### ❌ Out of Scope

- Treating utility classes as domain services.
- Enabling unrestricted polymorphism on untrusted JSON.
- Using Kit to hide transactions, network, or resource lifecycles.

## Workflow

1. Search the current Kit for an existing method.
2. Read the signature, implementation, and tests — do not infer semantics from names.
3. Distinguish pure functions, global mappers, and side-effecting utilities.
4. Pick the narrowest API; preserve `Optional`, exceptions, and generics.
5. Test boundary values and error paths.

## Common Mistakes

- Continuing to use the merged `JacksonKit` name.
- Using the Redis mapper to deserialize external payloads.
- Letting `BeanKit` silently copy where an explicit Domain-to-PO mapping is required.
- Hand-rolling logic that `StrKit` / `CollKit` already provide.
- Depending on high-line APIs without verifying older lines.
- Catching utility exceptions and returning false success.

## Output and Exceptions

Return the utility FQN, maintenance line, inputs and outputs, and null / exception semantics. When missing, return `missing: target type or maintenance line; how to provide: call site and POM`.

## Deep Reference

- [JSON and Jackson](references/json-and-jackson.md)
- [Bean, String, and Collection](references/bean-string-collection.md)
- [ID, Function, and Reflection](references/id-function-reflection.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

JSON, logs, and exceptions must not expose tokens, passwords, private fields, or private-repository credentials.

## Quick Start

- "Use `$ddd4j-kit` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-kit` to review existing usage against the current source."
- "Use `$ddd4j-kit` to return an implementation choice, evidence state, and remaining risk."

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
