# ddd4j-javalin 技能体系 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (- [ ]) syntax for tracking.

**Goal:** 建立 Javalin 版本、架构、运行时、认证、数据、Web、MQ、缓存、测试、发布和生产加固技能。

**Architecture:** 常规功能拆分；ddd4j-javalin-production-hardening 保留为跨能力交付工作流。Auth 统一 Sa-Token/Shiro/OIDC，Data 统一 MyBatis/JPA/PostgreSQL。

**Tech Stack:** Javalin 6/7、Java 17/21、Maven 3/4、Guice、Sa-Token、Shiro、OIDC、MyBatis、JPA、Testcontainers。

**Spec:** docs/superpowers/plans/2026-09-11-ddd4j-skills-plan.md

## Global Constraints

- 源码：/Users/wandl/workspaces/workspace-ddd4j/workspace-ddd4j-boot/ddd4j-javalin。
- 6.7.x、7.1.x、7.2.x 的完整版本元组分别验证。
- Javalin 6/7 API 不机械复制；smoke test 不替代真实 HTTP/Auth/DB 行为。
- 生产加固不替代日常功能技能。

## 计划技能

| 技能 | 统一覆盖 |
|---|---|
| ddd4j-javalin-version-selection | 6.7.x/7.1.x/7.2.x 完整版本元组 |
| ddd4j-javalin-architecture | parent/BOM/core/auth/data/mq/web/extensions/testcontainers |
| ddd4j-javalin-runtime | start、SPI、readiness、drain、rollback、close |
| ddd4j-javalin-auth | Sa-Token、Shiro、OIDC/Keycloak |
| ddd4j-javalin-data | MyBatis、JPA/PostgreSQL、Repository、事务 |
| ddd4j-javalin-web | 路由、Context、异常、CORS、幂等、请求限制 |
| ddd4j-javalin-mq | 注册、listener、ACK、重试、关闭 |
| ddd4j-javalin-cache | 本地/分布式缓存、CAS、幂等后端 |
| ddd4j-javalin-extensions | Guice Module、业务绑定和生命周期 |
| ddd4j-javalin-testing | HTTP、Keycloak、DB、Broker、Docker |
| ddd4j-javalin-release | 三线 Git、CI、私服和空缓存消费 |
| ddd4j-javalin-production-hardening | 跨能力审查、计划、TDD 和发布门禁 |

### Task 1: 版本与架构

**Files:** Create skills/ddd4j-javalin-version-selection/、skills/ddd4j-javalin-architecture/

- [ ] **Step 1:** 从三分支 POM、Wrapper、workflow、BuildLineContractTest 提取版本。
- [ ] **Step 2:** 固化 7.1.x Maven 3、7.2.x Maven 4 的证据。
- [ ] **Step 3:** 绘制模块和请求生命周期。
- [ ] **Step 4:** 用新项目、升级、维护三场景验证并提交。

### Task 2: runtime 与 web

**Files:** Create skills/ddd4j-javalin-runtime/、skills/ddd4j-javalin-web/

- [ ] **Step 1:** Runtime 覆盖 start→validate→initialize→ready→drain→close。
- [ ] **Step 2:** 覆盖部分失败反向回滚、hook 移除和幂等 close。
- [ ] **Step 3:** Web 覆盖 route、Context、错误、CORS、幂等、request size、async。
- [ ] **Step 4:** 分别验证 Javalin 6/7 HTTP contract 并提交。

### Task 3: auth

**Files:** Create skills/ddd4j-javalin-auth/ 及 references/framework-selection.md、satoken.md、shiro.md、oidc-keycloak.md、subject-lifecycle.md

- [ ] **Step 1:** 建立三框架选择矩阵。
- [ ] **Step 2:** 每框架说明依赖、配置、SubjectProvider、路由和错误。
- [ ] **Step 3:** Keycloak 要求取 Token、合法 200、缺失/非法 401/403。
- [ ] **Step 4:** 验证请求结束 Subject/Context 清理后提交。

### Task 4: data、mq、cache、extensions

**Files:** Create skills/ddd4j-javalin-data/、skills/ddd4j-javalin-mq/、skills/ddd4j-javalin-cache/、skills/ddd4j-javalin-extensions/

- [ ] **Step 1:** Data 统一 MyBatis/JPA/PostgreSQL、Repository、事务和 EMF。
- [ ] **Step 2:** MQ 覆盖 required/optional、ACK、重试、死信和关闭。
- [ ] **Step 3:** Cache 区分 Caffeine 与共享 CAS。
- [ ] **Step 4:** Extensions 说明 Module override 和生命周期后提交。

### Task 5: testing、release、production-hardening

**Files:** Create skills/ddd4j-javalin-testing/、skills/ddd4j-javalin-release/；Modify skills/ddd4j-javalin-production-hardening/SKILL.md

- [ ] **Step 1:** Testing 统一 HTTP、Keycloak、PostgreSQL、MQ 和 Docker 条件。
- [ ] **Step 2:** Release 固化三线最终 SHA、CI、私服和空缓存消费。
- [ ] **Step 3:** Production hardening 路由功能细节，保留计划审批、跨能力 TDD 和发布门禁。
- [ ] **Step 4:** 全量链接、TRACE、插件和 README 验证后提交。
