---
name: ddd4j-extensions
description: Use when choosing, integrating, or reviewing optional ddd4j extensions such as Excel, license, monitoring, OpenTelemetry, PF4J, QLExpress, QR code, validation, or Jackson-related integration boundaries.
license: Apache-2.0
---

# ddd4j Extensions

## Overview

Extensions are optional capabilities and must not pollute core in reverse. The current 3.0.x top-level extensions include Excel, License, Monitor, OTel, PF4J, QLExpress, QRCode, and Validation; Jackson core tooling lives in ddd4j-kit/core, and Akka currently lives mainly in ddd4j-boot.

## Selection Matrix

| Requirement | Extension |
|---|---|
| Excel | extension-excel |
| License | extension-license |
| Logging/alerting configuration | extension-monitor |
| Trace/metrics | extension-otel |
| Plugin system | extension-pf4j |
| Rule expressions | extension-qlexpress |
| QR codes | extension-qrcode |
| Extended validation | extension-validation |

## Core Rules

1. A missing classpath entry must not affect core.
2. Extensions provide framework-agnostic capabilities; Boot/Quarkus and others handle assembly.
3. Configuration switches, default implementations, user overrides, and close are explicit.
4. Do not present historical/Boot-only extensions as current core modules.
5. Prove each item with the current module and its tests.

## Capability Boundaries

### ✅ Strong At

- Extension selection and integration.
- Core/extension/runtime boundaries.
- Optional dependencies and lifecycle.
- Extension testing and degradation.

### ⚠️ Needs Input

- Current maintenance line and target runtime.
- Target extension and configuration.
- External service/license requirements.

### ❌ Out of Scope

- Claiming support for a module that does not exist.
- Extension dependencies leaking into core.
- Bypassing license validation.

## Deep Reference

- [Current Extensions](references/current-extensions.md)
- [Integration Pattern](references/integration-pattern.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

License, monitoring, plugin, and expression inputs can be sensitive; never log secrets, and sandbox rules/plugins behind allowlists.

## Quick Start

- "Use `$ddd4j-extensions` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-extensions` to review existing usage against the current source."
- "Use `$ddd4j-extensions` to return an implementation choice, evidence state, and remaining risk."

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
