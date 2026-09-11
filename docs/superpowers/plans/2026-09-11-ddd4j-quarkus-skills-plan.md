# ddd4j-quarkus 技能体系 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (- [ ]) syntax for tracking.

**Goal:** 建立 Quarkus 版本、扩展开发、CDI、认证、数据、Web、MQ、缓存、测试和发布技能。

**Architecture:** 构建期 extension-authoring 独立；runtime CDI 与功能适配分别建技能。Data 覆盖 Panache/JPA/JDBI/R2DBC，Auth 覆盖 JWT/OIDC/Shiro/Sa-Token 的真实支持边界。

**Tech Stack:** Quarkus、CDI/Arc、BuildItem、Recorder、Panache、JAX-RS、OIDC/JWT、Testcontainers、Maven 3/4。

**Spec:** docs/superpowers/plans/2026-09-11-ddd4j-skills-plan.md

## Global Constraints

- 源码：/Users/wandl/workspaces/workspace-ddd4j/workspace-ddd4j-boot/ddd4j-quarkus。
- 3.3.x/4.0.x 的 ddd4j、JDK、Maven、POM Model、Quarkus 分别验证。
- runtime/deployment、CDI scope、Recorder、BuildItem 不用 Spring 模型解释。
- Security skip 记为 SKIPPED 风险。

## 计划技能

| 技能 | 统一覆盖 |
|---|---|
| ddd4j-quarkus-version-selection | 3.3.x/4.0.x、ddd4j、JDK、Maven、Quarkus |
| ddd4j-quarkus-architecture | parent/BOM/extension-parent/auth/data/mq/web/cache |
| ddd4j-quarkus-extension-authoring | runtime/deployment、BuildItem、Recorder、配置 |
| ddd4j-quarkus-runtime | CDI、CommandBus、Publisher、SubjectProvider、Context |
| ddd4j-quarkus-auth | JWT、OIDC、Shiro、Sa-Token 支持边界 |
| ddd4j-quarkus-data | Panache、JPA、JDBI、R2DBC、事务、租户 |
| ddd4j-quarkus-web | JAX-RS、Context、错误、认证、幂等 |
| ddd4j-quarkus-mq | Kafka、NATS、其他 MQ 和容器 |
| ddd4j-quarkus-cache | Quarkus Cache、Redis、ddd4j Cache SPI |
| ddd4j-quarkus-testing | QuarkusTest、TestResource、Arc、Docker/ClassLoader |
| ddd4j-quarkus-release | 双线 CI、Maven 4、私服和空缓存消费 |

### Task 1: 版本与架构

**Files:** Create skills/ddd4j-quarkus-version-selection/、skills/ddd4j-quarkus-architecture/

- [ ] **Step 1:** 从两分支 POM、Wrapper 和 workflow 提取版本元组。
- [ ] **Step 2:** 区分当前 patch、后续稳定线和未验证前瞻版本。
- [ ] **Step 3:** 解释 parent/dependencies/BOM/extension-parent。
- [ ] **Step 4:** 用新项目和已有项目场景验证并提交。

### Task 2: extension-authoring 与 runtime

**Files:** Create skills/ddd4j-quarkus-extension-authoring/、skills/ddd4j-quarkus-runtime/

- [ ] **Step 1:** 提取 runtime/deployment 配对、processor、BuildItem、Recorder。
- [ ] **Step 2:** 写明 CDI bean-defining scope、Arc validation、native image。
- [ ] **Step 3:** Runtime 覆盖 CommandBus、Publisher、SubjectProvider、上下文和关闭。
- [ ] **Step 4:** 验证启动、重复注册、请求清理后提交。

### Task 3: auth、data、cache

**Files:** Create skills/ddd4j-quarkus-auth/、skills/ddd4j-quarkus-data/、skills/ddd4j-quarkus-cache/

- [ ] **Step 1:** Auth 建立 JWT/OIDC/Shiro/Sa-Token 支持矩阵，未实现项明确标注。
- [ ] **Step 2:** 验证 JWT Subject、SubjectKit、SubjectProvider 同请求一致。
- [ ] **Step 3:** Data 统一 Panache/JPA/JDBI/R2DBC、复合键、租户和事务。
- [ ] **Step 4:** Cache 比较 Quarkus Cache、Redis、ddd4j SPI 后提交。

### Task 4: web 与 mq

**Files:** Create skills/ddd4j-quarkus-web/、skills/ddd4j-quarkus-mq/

- [ ] **Step 1:** Web 覆盖 JAX-RS、Context、异常、Auth、幂等和 HTTP contract。
- [ ] **Step 2:** MQ 覆盖 Kafka、NATS 和其他当前实现的生命周期。
- [ ] **Step 3:** 不把 BOM 引入当运行时 Bean 已装配。
- [ ] **Step 4:** 执行 round-trip 或明确 BLOCKED 后提交。

### Task 5: testing 与 release

**Files:** Create skills/ddd4j-quarkus-testing/、skills/ddd4j-quarkus-release/

- [ ] **Step 1:** Testing 覆盖 QuarkusTest、TestResource、Arc、Docker/ClassLoader。
- [ ] **Step 2:** 保留 docker info 优先、DockerClientFactory 回退语义。
- [ ] **Step 3:** Release 记录双线 Maven 3/4、CI、Security、私服和空缓存消费。
- [ ] **Step 4:** 更新插件、README、TRACE 和远端 SHA 后提交。
