---
name: ddd4j-javalin-production-hardening
description: Use when hardening or releasing ddd4j-javalin 6.7.x, 7.1.x, or 7.2.x across runtime lifecycle, readiness, configuration, idempotency, CORS, multi-branch TDD, CI, or private Maven workflows.
---

# DDD4J Javalin Production Hardening

## Purpose

Turn a `ddd4j-javalin` hardening request into an evidence-backed delivery without collapsing review, planning, implementation, CI, publication, and production acceptance into one status.

## Quick start

Typical requests:

- "Use `$ddd4j-javalin-production-hardening` to review the production-readiness gaps of the three Javalin branches and update the existing plan."
- "Complete runtime/readiness/CORS hardening with TDD according to the approved Phase D plan."
- "Check CI on the three branches, publish to the Alibaba Cloud private Maven repository, and finish with a clean-cache consumption verification."

Start by locating the real repository and reading current evidence. Do not assume the historical branch matrix, plan state, remote state, or credentials are still current.

## Capability boundaries

### Good fit

- Review Javalin runtime/bootstrap, lifecycle, readiness, configuration, CORS, idempotency, persistence, and shutdown behavior.
- Update an existing approved Javalin specification or Superpowers plan, then execute it with failing contracts first.
- Carry one approved behavior change across the three maintenance lines while preserving line-specific toolchains.
- Inspect GitHub Actions and execute an explicitly authorized private Maven release with remote-consumer proof.

### Needs project evidence or authorization

- Implementation needs the repository, current branch/worktree state, applicable instructions, and the active plan/specification.
- Push, branch switching, commit, private publication, or credential use needs the corresponding user authorization.
- Production claims need runtime/operational evidence; source and test results alone are insufficient.

### Out of scope

- Generic `ddd4j`, Boot, Quarkus, or Cloud release work unless it is a verified Javalin dependency blocker.
- Silently initializing Spec Kit/OpenSpec, creating a second specification, changing GitHub billing, or rotating secrets.
- Treating a CI start, artifact upload, HTTP 200, or local build as production acceptance.

## Required discovery

Before edits, report the SDD state and perform read-only discovery:

1. Resolve the exact repo root and target module; inspect `git status --short --branch`, `git worktree list`, local/remote refs, and dirty files.
2. Read applicable `AGENTS.md`, `CLAUDE.md`, README, branch/POM matrix, and the current specification, plan, tasks, and status report.
3. Detect `.specify/`, `openspec/`, and `docs/superpowers/{specs,plans}`. Continue the existing fact source. If both Spec Kit and OpenSpec are active for the same change and ownership is unclear, stop before creating artifacts and ask the user to choose.
4. If `.codegraph/` exists, use CodeGraph before grep for runtime entrypoints, lifecycle ownership, readiness contributors, and shutdown call paths.
5. Re-derive the current branch contract from POMs, wrappers, CI workflows, and tests. Historical defaults are only hypotheses:

| Line | Expected dependency line | Expected Javalin | Toolchain hypothesis |
|---|---|---|---|
| `feature/6.7.x` | ddd4j 1.0.x | 6.7.0 | JDK 17, Maven 3, POM 4.0/modules |
| `feature/7.1.x` | ddd4j 2.0.x | 7.1.0 | JDK 17, Maven 3, POM 4.0/modules |
| `feature/7.2.x` | ddd4j 3.0.x | 7.2.3 | JDK 21, Maven 4, POM 4.1/subprojects |

Read [references/workflow.md](references/workflow.md) before planning or implementation. Read [references/release-gates.md](references/release-gates.md) before CI, push, deploy, or release-status work.

## Audience, routing, and customization

- Maintainers use review mode to audit production gaps and current plan truth without modifying code.
- Implementers use execution mode only after the plan is approved; it follows contract-first TDD and per-line adaptation.
- Release engineers use release mode for final-SHA CI inspection, serial private publication, and isolated consumption proof.
- Reviewers use verification mode to challenge claimed evidence without pushing or publishing.

Infer the mode from the request. If multiple modes are requested, preserve the order `review → plan approval → execute → verify → release`. Accept user constraints such as target branches, excluded modules, required CI jobs, private repository name, security-waiver status, and whether commit/push/deploy are authorized. These parameters override historical defaults but not current repository evidence or safety boundaries.

When required material is missing, report it as "missing: specific project/branch/specification/authorization/credential source; how to provide: state the path or authorization scope". Continue all safe read-only checks and give a provisional result instead of returning an empty response.

## Decision rules

- Keep the request Javalin-only. Escalate an upstream dependency only when current evidence proves it blocks Javalin.
- Review first. If the user says "write the plan first, execute later", update the existing plan and pause implementation until plan approval is explicit.
- Do not copy code mechanically across lines. Preserve Javalin 6 versus 7 APIs, Java syntax, Maven model, and dependency contracts.
- Convert each risk into an observable contract: fail first, implement the smallest behavior, then run focused and affected regression tests.
- Keep evidence tiers separate: source review → focused tests → per-line clean reactor → runtime/container tests → Git/remote SHA → CI → private publication → isolated remote consumption → production acceptance.
- Never expose repository credentials, settings files, tokens, private URLs containing secrets, or raw environment values. Report only credential presence/source and redact sensitive output.

## Capability skill routing

Detailed implementations are handed off separately to `ddd4j-javalin-runtime`, `ddd4j-javalin-auth`, `ddd4j-javalin-data`, `ddd4j-javalin-web`, `ddd4j-javalin-mq`, `ddd4j-javalin-cache`, `ddd4j-javalin-testing`, and `ddd4j-javalin-release`. This skill retains only cross-capability review, plan approval, TDD orchestration, and production release gates.

## Hardening model

Investigate these concerns when relevant; do not force them into unrelated work:

- `Ddd4jJavalinRuntime`: coherent `start → validate → initialize → ready → drain → close`, rollback after partial initialization, and idempotent close.
- `JavalinLifecycleParticipant`: ordered initialization, readiness contribution, reverse-order shutdown, and clear required-versus-optional dependency semantics.
- Real configuration loading and startup validation instead of default-object construction plus port parsing.
- Aggregated readiness for dependencies such as database, MQ, OIDC, Outbox, and repository initialization; liveness must remain distinct.
- Shared CAS-backed idempotency for multi-instance production; Caffeine is an explicit single-instance/development fallback.
- Explicit CORS origin, credential, header, and method policy; no production `anyHost()` shortcut.
- Ownership and shutdown for JPA `EntityManagerFactory`, schedulers, listeners, and core runtime.
- Shutdown-hook registration/removal that does not accumulate during repeated starts or embedded tests.

## Output contract

At the start of non-trivial work, state: project type, detected SDD systems, fact source, current phase, execution method, next step, and whether files will change.

At handoff, state:

- active specification/plan and task status;
- changes per branch and exact local/tracking/remote SHAs;
- tests actually run, toolchain used, counts/results, and skipped gates;
- CI run/job conclusions, not merely run creation;
- publication coordinates and isolated empty-cache consumer evidence;
- unresolved compatibility, security, infrastructure, and production-acceptance risks.

Use explicit states such as `PASS`, `FAIL`, `BLOCKED`, `SKIPPED`, and `NOT RUN`. Never translate `BLOCKED` or `SKIPPED` into success.

## Common questions

1. **Can an existing plan be replaced?** No. Extend the active fact source unless the user authorizes migration or replacement.
2. **Can all lines use Maven 4?** No. Derive and preserve each line's current core/POM contract.
3. **Is a focused test enough?** It proves only that contract; run affected regression and the appropriate per-line gate.
4. **Does a push mean CI passed?** No. Resolve the run for the exact SHA and wait for terminal job conclusions.
5. **Does `deploy` upload activity mean release success?** No. Require a zero exit code, complete module inventory, remote metadata/integrity checks, and clean-cache consumption.
6. **What if Actions is blocked by billing?** Mark CI `BLOCKED`; do not change billing or secrets. Use local publication only when the user authorized it.

For failure patterns and edge cases, read [references/anti-patterns-and-faq.md](references/anti-patterns-and-faq.md).

## Deep Reference

- [Source Evidence Routing](references/source-evidence.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)
