# ddd4j-boot 技能体系 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (- [ ]) syntax for tracking.

**Goal:** 从 ddd4j-boot 当前维护线与功能模块创建按功能域组织的 Spring Boot 技能组。

**Architecture:** 版本、架构、自动配置、功能集成、测试和发布分别建技能；每个功能技能覆盖域内多实现，不按 starter artifact 建技能。

**Tech Stack:** Spring Boot 2.3–4.1、Java 8/17/21、Maven 3/4、AutoConfiguration、Testcontainers。

**Spec:** docs/superpowers/plans/2026-09-11-ddd4j-skills-plan.md

## Global Constraints

- 源码：/Users/wandl/workspaces/workspace-ddd4j/workspace-ddd4j-boot/ddd4j-boot。
- 版本事实从 config/consistency/ddd4j-boot-build-matrix.tsv、13 条 POM、Wrapper 和 workflow 重建。
- Boot 2.x/3.x/4.x 的 JDK、Maven、POM Model 分别验证。
- 条件装配、用户 Bean 覆盖、配置属性、资源注册和销毁需要测试证据。

## 计划技能

| 技能 | 统一覆盖 |
|---|---|
| ddd4j-boot-version-selection | 13 条 Boot→ddd4j→JDK/Maven/POM 组合 |
| ddd4j-boot-architecture | parent/BOM 与 core/auth/data/mq/web/cache/extensions 分层 |
| ddd4j-boot-bom | parent、dependencies、effective POM 和版本所有权 |
| ddd4j-boot-autoconfiguration | 条件、Properties、用户覆盖、注册和销毁 |
| ddd4j-boot-auth | Sa-Token、Shiro、Spring Security |
| ddd4j-boot-data | JDBC、JPA、MyBatis、Plus、迁移、事务 |
| ddd4j-boot-mq | 多 Broker、listener、ACK、重试、生命周期 |
| ddd4j-boot-web | MVC、WebFlux、Context、异常、认证、幂等 |
| ddd4j-boot-cache | 本地、Redis、Redisson、JetCache、CAS |
| ddd4j-boot-observability | Actuator、metrics、trace、logging、readiness |
| ddd4j-boot-extensions | Akka、Excel、QLExpress、QRCode、Monitor |
| ddd4j-boot-testing | ContextRunner、slice、matrix、Testcontainers |
| ddd4j-boot-release | 13 线构建、CI、私服、空缓存消费 |

### Task 1: 版本、架构和 BOM

**Files:** Create skills/ddd4j-boot-version-selection/、skills/ddd4j-boot-architecture/、skills/ddd4j-boot-bom/

- [ ] **Step 1:** 提取 13 条 Boot→ddd4j→JDK/Maven/POM 完整矩阵。
- [ ] **Step 2:** 标明主组合、备选、不兼容和未验证。
- [ ] **Step 3:** 解释 parent/dependencies/BOM 与具体模块的所有权。
- [ ] **Step 4:** 用 Boot 2.7、3.5、4.1 三场景验证并提交。

### Task 2: 自动配置与 extensions

**Files:** Create skills/ddd4j-boot-autoconfiguration/、skills/ddd4j-boot-extensions/

- [ ] **Step 1:** 提取 ConditionalOnClass/MissingBean/Property、Properties、imports 模式。
- [ ] **Step 2:** 比较 Boot 2 旧注册与新 AutoConfiguration imports。
- [ ] **Step 3:** Extensions 统一 Akka、Excel、QLExpress、QRCode、Monitor 等实现。
- [ ] **Step 4:** 验证开关、用户覆盖和 destroyMethod 后提交。

### Task 3: auth、data、cache

**Files:** Create skills/ddd4j-boot-auth/、skills/ddd4j-boot-data/、skills/ddd4j-boot-cache/

- [ ] **Step 1:** Auth 比较 Sa-Token、Shiro、Spring Security 的 Boot 装配。
- [ ] **Step 2:** Data 比较 JDBC、JPA、MyBatis、Plus、迁移和事务。
- [ ] **Step 3:** Cache 比较本地、Redis、Redisson、JetCache 及 CAS。
- [ ] **Step 4:** 增加各 Boot 代际最小启动测试并提交。

### Task 4: mq、web、observability

**Files:** Create skills/ddd4j-boot-mq/、skills/ddd4j-boot-web/、skills/ddd4j-boot-observability/

- [ ] **Step 1:** MQ 覆盖多 Broker、listener、ACK、重试、启动和反向关闭。
- [ ] **Step 2:** Web 覆盖 MVC/WebFlux、Context、异常、Auth、幂等、readiness。
- [ ] **Step 3:** Observability 覆盖 Actuator、metrics、trace 和日志。
- [ ] **Step 4:** 使用真实 HTTP/Broker/Actuator 证据校正并提交。

### Task 5: testing 与 release

**Files:** Create skills/ddd4j-boot-testing/、skills/ddd4j-boot-release/

- [ ] **Step 1:** Testing 覆盖 ApplicationContextRunner、slice、matrix、Testcontainers。
- [ ] **Step 2:** 区分 Docker 不可用、skip、零测试与 PASS。
- [ ] **Step 3:** Release 覆盖 13 线 clean build、最终 SHA、CI、私服和空缓存消费。
- [ ] **Step 4:** 更新插件、README、TRACE 和安装发现后提交。
