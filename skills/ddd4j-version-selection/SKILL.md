---
name: ddd4j-version-selection
description: Use when choosing compatible ddd4j, ddd4j-boot, ddd4j-cloud, ddd4j-javalin, or ddd4j-quarkus versions for a new project, upgrade, migration, or maintained release line.
license: Apache-2.0
---

# ddd4j Version Selection

## Overview

What gets selected is a complete compatibility tuple, not a single "latest version". Fix the JDK, build tool, and runtime first, then choose ddd4j and the adapter project.

## Quick Start

- "Which ddd4j line should a JDK 17 Spring Boot 3.4 project pick?"
- "Can Javalin 7.1 use ddd4j 3.0.x?"
- "Which Boot and ddd4j versions correspond to Spring Cloud 2024.0.x?"
- "Why does Quarkus 4.0.x still use Quarkus 3.38?"

## Input Contract

Collect at least:

1. Whether the project is new, an upgrade, or maintenance.
2. Available JDK and Maven versions.
3. Target Spring Boot/Cloud, Javalin, or Quarkus versions.
4. Whether POM 4.0/Maven 3 is mandatory.
5. Whether remote SNAPSHOT consumption and verified CI are required.

When input is missing, give a tentative candidate first, then output "missing: specific constraint; how to provide: supply the POM, java -version, mvn -version".

## Decision Order

1. Lock the ddd4j main line by JDK: Java 8→1.0.x, Java 17→2.0.x, Java 21→3.0.x.
2. Lock the adapter project maintenance line by runtime.
3. Verify the Maven/POM Model: 1.x/2.x are usually Maven 3/POM 4.0; 3.x is Maven 4/POM 4.1.
4. Verify the exact upstream framework version.
5. Query private Maven repository metadata and the final SHA; mark NOT VERIFIED when unverified.
6. Output four categories: recommended, alternative, incompatible, unverified.

## Quick Matrix

| ddd4j | JDK | Maven/POM | Boot |
|---|---:|---|---|
| 1.0.x | 8 | Maven 3 / 4.0.0 | Boot 2.3–2.7 |
| 2.0.x | 17 | Maven 3 / 4.0.0 | Boot 3.0–3.5 |
| 3.0.x | 21 | Maven 4 / 4.1.0 | Boot 4.0–4.1 |

For the full Boot, Cloud, Javalin, and Quarkus matrices, see the [Compatibility Matrix](references/compatibility-matrix.md).

## Output Format

| Field | Content |
|---|---|
| Recommended combination | JDK, Maven, POM, ddd4j, adapter project, framework |
| Selection rationale | Matched source matrix and constraints |
| Incompatible items | Conflicting fields and reasons |
| Evidence status | SOURCE / TEST / CI / PUBLISHED / CONSUMED |
| Follow-up verification | Exact commands, branches, and coordinates |

## Capability Boundaries

### ✅ Strong At

- Version combination selection across the five repositories.
- The Maven 3/4 and POM 4.0/4.1 boundary.
- Primary combinations, compatible alternatives, and upgrade paths.
- Distinguishing local success from remote consumability.

### ⚠️ Needs Input

- Current POM, branch, or target framework version.
- Private repository access conditions.
- Whether historical lines may upgrade JDK/Maven.

### ❌ Out of Scope

- Guessing that unreleased versions work.
- Automatically upgrading dependencies or switching branches.
- Substituting branch names for POM, CI, and remote evidence.

## Common Mistakes

1. Recommending the highest ddd4j main line to every project.
2. Promoting Javalin 7.1.x to Maven 4.
3. Treating the Quarkus adapter version as the Quarkus Platform version.
4. Reading only the Cloud branch name without checking the Boot parent.
5. Treating the start of a deploy upload as a finished release.
6. Writing Security SKIPPED down as PASS.

## Deep Reference

- [Compatibility Matrix](references/compatibility-matrix.md)
- [Evidence and Gates](references/evidence-and-gates.md)
- [Anti-Patterns](references/anti-patterns.md)
- [Deep FAQ](references/faq-deep.md)

## Privacy and Security

Never output Maven settings, tokens, passwords, or credentialed private repository URLs; report only credential sources and redacted errors.

## Audience and Customization

- New project developers provide the JDK and target runtime.
- Maintainers provide the existing POM, branch, and upgrade constraints.
- Release engineers specify CI/private repository/clean-cache evidence requirements.

Customize the target product, allowed maintenance lines, and evidence level. When input is insufficient, give a tentative combination first, then list "missing: version constraints; how to provide: supply the POM and tool versions".

## FAQ

1. **Is the latest version always chosen?** No — constraints come first.
2. **Is picking just the ddd4j version enough?** No — the full tuple is required.
3. **Can a branch name prove the framework version?** No.
4. **Does a local SNAPSHOT count as available?** It is not remotely available.
5. **What if CI never started?** Mark BLOCKED.
6. **What if the matrix is stale?** Refresh the current POMs and verification scripts.
