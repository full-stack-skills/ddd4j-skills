---
name: ddd4j-auth
description: Use when choosing, integrating, or reviewing ddd4j authentication and authorization with Sa-Token, Apache Shiro, or Spring Security, including Subject mapping, roles, permissions, sessions, temporary tokens, and exception handling.
license: Apache-2.0
---

# ddd4j Auth

## Overview

All three frameworks map onto the ddd4j Subject/AuthPrincipal/SubjectProvider; domain and application code never binds directly to a concrete security context.

## Framework Selection

| Scenario | Recommendation |
|---|---|
| Multiple account types, temporary tokens, lightweight domestic projects | Sa-Token |
| Existing Realm/Subject/Permission | Shiro |
| Spring enterprise security, OAuth2/OIDC, method security | Spring Security |

## Unified Chain

Authentication framework → SubjectProvider → ddd4j Subject → AuthPrincipal → request Context → application/domain services.

Each implementation must state its dependencies, configuration, identity mapping, roles and permissions, exceptions, context cleanup, and tests.

## Capability Boundaries

### ✅ Strong At

- The Subject/AuthPrincipal/Provider abstraction.
- Selecting and using Sa-Token, Shiro, and Spring Security.
- Temporary tokens, API keys, roles and permissions.
- Request lifecycle and exception mapping.

### ⚠️ Needs Input

- Current maintenance line, runtime, and authentication framework.
- Token/Session mode and account model.
- Roles, permissions, tenants, and logout requirements.

### ❌ Out of Scope

- Bypassing authentication or operating another user's account.
- Treating Same-Token as an end-user token.
- Reading SecurityContext/StpUtil/Shiro SecurityUtils in the domain layer.

## Workflow

1. Select the framework and confirm the actual artifacts.
2. Define the AuthPrincipal profile, roles, and permissions.
3. Implement/assemble the SubjectProvider.
4. Bind at request start; restore/clean up at request end.
5. Convert framework exceptions into stable web errors.
6. Test anonymous, valid, expired, insufficient-role, thread-reuse, and logout paths.

## Common Mistakes

- Assembling all three frameworks at once and fighting over the SubjectProvider.
- Hardcoding Sa-Token extra keys.
- Leaving SecurityContext/Shiro Subject uncleaned.
- Testing only successful login and never the request end.
- Logging full tokens/API keys.
- Treating a BOM dependency as proof that authentication is enabled.

## Output and Exceptions

Output the framework choice, artifacts, configuration, Subject mapping, lifecycle, and tests. When input is missing, write "missing: authentication framework/mode/runtime; how to provide: supply the POM and redacted configuration".

## Deep Reference

- [Framework Selection](references/framework-selection.md)
- [Sa-Token](references/satoken.md)
- [Shiro](references/shiro.md)
- [Spring Security](references/spring-security.md)
- [Subject Lifecycle](references/subject-lifecycle.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Use fictional identities only; tokens, API keys, sessions, and organization/role data must be redacted.

## Quick Start

- "Use `$ddd4j-auth` to analyze the implementation and configuration my current project should adopt."
- "Use `$ddd4j-auth` to review existing usage against the current source."
- "Use `$ddd4j-auth` to return an implementation choice, evidence state, and remaining risk."

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
