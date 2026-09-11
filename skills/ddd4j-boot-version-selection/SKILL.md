---
name: ddd4j-boot-version-selection
description: Use when choosing a compatible ddd4j-boot maintenance line for a Spring Boot project, upgrade, or legacy system based on Spring Boot, ddd4j, JDK, Maven, and POM model constraints.
license: Apache-2.0
---

# ddd4j-boot 版本选择

## Overview

以 Spring Boot 版本和 JDK 为入口，输出 Boot→ddd4j→JDK→Maven/POM 完整元组。

## 快速矩阵

| Boot | ddd4j | JDK | Maven/POM |
|---|---|---:|---|
| 2.3–2.7 | 1.0.x | 8 | Maven 3 / 4.0 |
| 3.0–3.5 | 2.0.x | 17 | Maven 3 / 4.0 |
| 4.0–4.1 | 3.0.x | 21 | Maven 4 / 4.1 |

精确 patch 见 [13 条维护线](references/maintenance-matrix.md)。

## 决策规则

1. 已有项目先尊重当前 Spring Boot/JDK。
2. 新项目选择组织支持且远端可消费的最高主组合。
3. 不跨 ddd4j 主线混用 parent/BOM。
4. Boot 4 需要 Maven 4/POM 4.1/subprojects。
5. 输出 SOURCE/TEST/CI/PUBLISHED/CONSUMED 证据状态。

## 能力边界

### ✅ 擅长

- 13 条维护线选择。
- 升级路径和不兼容解释。
- JDK/Maven/POM 约束。
- 远端消费门禁。

### ⚠️ 需要素材

- Spring Boot/JDK/Maven。
- 当前 parent/BOM。
- 私服和 CI 要求。

### ❌ 超范围

- 自动升级源码。
- 猜测未发布坐标。
- 用本地缓存证明远端可用。

## 深度参考

- [维护矩阵](references/maintenance-matrix.md)
- [选择与升级](references/selection-and-upgrade.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出 Maven settings 或私服凭据。

