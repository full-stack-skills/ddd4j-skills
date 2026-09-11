# ddd4j 核心技能体系 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (- [ ]) syntax for tracking.

**Goal:** 以当前 ddd4j 源码为事实源，建立版本选择和按功能域组织的核心技能体系，并合并粒度过细的框架专项入口。

**Architecture:** ddd4j-version-selection 是全库首入口；其他技能按用户决策域组织。每个功能技能用简洁 SKILL.md 路由到同目录 references 中的多实现指南，不按 Maven artifact 一包一技能。

**Tech Stack:** Agent Skills、Markdown、YAML、CodeGraph、Maven、Git、TRACE。

**Spec:** 本文件“规划基线（用户已确认）”。

## Global Constraints

- 事实源：/Users/wandl/workspaces/workspace-ddd4j/workspace-ddd4j-boot/ddd4j 的目标维护线源码、POM、测试和 CodeGraph。
- 区分 JDK、Maven、POM Model、依赖版本、源码、测试、CI、发布和生产验收。
- SKILL.md 少于 500 行；多实现细节放在一层 references。
- 新入口验证完成后才能删除旧入口。
- 每个新技能执行无技能基线场景、带技能场景、链接检查和 TRACE。

## 规划基线（用户已确认）

| 技能 | 必须统一覆盖 |
|---|---|
| ddd4j-version-selection | ddd4j、Boot、Cloud、Javalin、Quarkus 完整兼容元组 |
| ddd4j-architecture | DDD/CQRS、模块依赖、六边形和运行时边界 |
| ddd4j-annotation | DDD、CQRS、API、ORM 注解及扫描语义 |
| ddd4j-bom | parent、dependencies、BOM 所有权、Maven 3/4 |
| ddd4j-core | AggregateRoot、Command、Query、DomainEvent、Repository、Context |
| ddd4j-auth | Subject/AuthPrincipal；Sa-Token、Shiro、Spring Security |
| ddd4j-data | JDBC、JDBI、JPA、MyBatis、MyBatis-Plus、R2DBC、Panache、EventStore、Projection、Outbox |
| ddd4j-mq | Kafka、RabbitMQ、Pulsar、RocketMQ、ActiveMQ、Artemis、MQTT、NATS、SQS、Spring Cloud Stream |
| ddd4j-kit | JsonKit、BeanKit、StrKit、CollKit、IdKit |
| ddd4j-web | MVC、WebFlux、Javalin、Quarkus REST、Micronaut、Vert.x、Helidon、Dropwizard、Validation、Auth、Idempotency、CORS、Readiness |
| ddd4j-cache | Caffeine、Guava、Hutool、Redis、Redisson、Lettuce、Jedis、Memcached、JetCache |
| ddd4j-metrics | Core/Projection/Web/MQ/Runtime 指标 |
| ddd4j-runtime | Spring、Guice、Quarkus CDI、上下文、SPI、总线、发布器、初始化/回滚/关闭 |
| ddd4j-extensions | Jackson、Excel、Akka、PF4J、QLExpress、QR Code、Monitor |

### Task 1: 创建 ddd4j-version-selection

**Files:**
- Create: skills/ddd4j-version-selection/SKILL.md
- Create: skills/ddd4j-version-selection/references/compatibility-matrix.md
- Create: skills/ddd4j-version-selection/references/evidence-and-gates.md
- Create: skills/ddd4j-version-selection/references/anti-patterns.md
- Create: skills/ddd4j-version-selection/references/faq-deep.md

**Interfaces:**
- Consumes: 五仓库 POM、Wrapper、workflow、矩阵和远端制品证据。
- Produces: 推荐、备选、不兼容、未验证四态的完整版本元组。

- [x] **Step 1:** 写三个失败基线：盲选最新版、旧线误用 Maven 4、未发布坐标被称为可用。
- [x] **Step 2:** 创建只描述触发条件的 frontmatter，并在正文收集 JDK、Maven、运行时、现有版本和项目类型。
- [x] **Step 3:** 逐行写入来源路径、SHA、验证级别和日期。
- [x] **Step 4:** 用 Boot、Cloud、Javalin、Quarkus 各一个场景验证完整元组输出。
- [x] **Step 5:** TRACE 后提交：feat: 添加 ddd4j 版本选择技能。

### Task 2: 创建 architecture、annotation、bom

**Files:**
- Create: skills/ddd4j-architecture/
- Create: skills/ddd4j-annotation/
- Create: skills/ddd4j-bom/

- [x] **Step 1:** CodeGraph 提取模块调用方向、注解消费者和版本所有权。
- [x] **Step 2:** architecture 只讲边界；annotation 只讲语义与扫描；bom 只讲版本治理。
- [x] **Step 3:** 验证领域层依赖框架、重复注解、版本泄漏和 Model 4.1 错用场景。
- [x] **Step 4:** 更新插件/README，TRACE 后提交。

### Task 3: 重构 core 与创建 kit

**Files:**
- Modify: skills/ddd4j-core/SKILL.md
- Create: skills/ddd4j-kit/
- Delete after migration: skills/ddd4j-jackson/

- [x] **Step 1:** core 保留聚合、CQRS、事件、仓储和上下文，其他内容只路由。
- [x] **Step 2:** kit 覆盖 JsonKit、BeanKit、StrKit、CollKit、IdKit 和 Jackson 安全边界。
- [x] **Step 3:** 验证所有旧 Jackson 场景由 kit 或 data reference 接管。
- [x] **Step 4:** 删除旧入口、检查断链并提交。

### Task 4: 创建 auth 与 cache

**Files:**
- Create: skills/ddd4j-auth/
- Create: skills/ddd4j-auth/references/satoken.md
- Create: skills/ddd4j-auth/references/shiro.md
- Create: skills/ddd4j-auth/references/spring-security.md
- Create: skills/ddd4j-auth/references/framework-selection.md
- Create: skills/ddd4j-cache/
- Delete after migration: skills/ddd4j-satoken/

- [x] **Step 1:** Auth 先讲统一 Subject/AuthPrincipal，再比较三框架。
- [x] **Step 2:** 每框架覆盖依赖、配置、身份映射、权限、异常、上下文清理和测试。
- [x] **Step 3:** Cache 覆盖本地/分布式实现、TTL、CAS 和集群幂等。
- [x] **Step 4:** 验证 Sa-Token 场景完整迁移后删除旧入口并提交。

### Task 5: 创建 data 与 mq

**Files:**
- Create: skills/ddd4j-data/
- Create: skills/ddd4j-mq/
- Delete after migration: skills/ddd4j-mybatis/

- [x] **Step 1:** Data 建立 JDBC/JDBI/JPA/MyBatis/Plus/R2DBC/Panache 选择矩阵。
- [x] **Step 2:** 单列 EventStore、Projection、Outbox 的事务和一致性边界。
- [x] **Step 3:** MQ 建立 Broker、ACK、重试、死信、幂等、生命周期和 Testcontainers 章节。
- [x] **Step 4:** 使用真实数据库/Broker测试报告校正陈述并提交。

### Task 6: 创建 web、metrics、runtime、extensions

**Files:**
- Create: skills/ddd4j-web/
- Create: skills/ddd4j-metrics/
- Create: skills/ddd4j-runtime/
- Create: skills/ddd4j-extensions/
- Delete after migration: skills/ddd4j-validation/

- [x] **Step 1:** Web 统一多运行时响应、上下文、认证、幂等、CORS 和 readiness。
- [x] **Step 2:** Validation 迁入 web/references/validation.md。
- [x] **Step 3:** Runtime 比较 Spring/Guice/Quarkus CDI 的 SPI 与生命周期。
- [x] **Step 4:** Extensions 按功能介绍 Jackson/Excel/Akka/PF4J/QLExpress/QR/Monitor。
- [x] **Step 5:** 全量场景、TRACE、插件、README 和安装发现验证后提交。
