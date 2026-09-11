# ddd4j-cloud 技能体系 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (- [ ]) syntax for tracking.

**Goal:** 建立 Cloud 版本、上下文、租户、Feign、Stream、Web、数据、观测、测试和发布技能。

**Architecture:** Cloud 技能只描述 Spring Cloud 专有集成；Stream 统一多个 Binder，Web 统一 MVC/WebFlux，版本技能维护 Cloud→Boot→ddd4j 三层关系。

**Tech Stack:** Spring Cloud、Boot、Stream、Feign、Nacos、Sentinel、Seata、Testcontainers、Maven。

**Spec:** docs/superpowers/plans/2026-09-11-ddd4j-skills-plan.md

## Global Constraints

- 源码：/Users/wandl/workspaces/workspace-ddd4j/workspace-ddd4j-cloud/ddd4j-cloud。
- 读取现有 OpenSpec，但不修改其规格。
- 区分主组合与兼容备选；不得混用旧 cmpt 与新 extensions 命名。
- 多 Broker 的 destination、ACK 和容器证据分别陈述。

## 计划技能

| 技能 | 统一覆盖 |
|---|---|
| ddd4j-cloud-version-selection | Cloud→Boot→ddd4j→JDK/Maven |
| ddd4j-cloud-architecture | parent/BOM/extensions/samples/verification |
| ddd4j-cloud-bom | Cloud、Boot、ddd4j BOM 顺序与所有权 |
| ddd4j-cloud-context | 请求头、线程、异步和 Feign 传播 |
| ddd4j-cloud-tenant | Tenant、系统隔离和数据范围 |
| ddd4j-cloud-data | datasource、MyBatis/JPA、事务、Seata |
| ddd4j-cloud-feign | interceptor、error decoder、重试、清理 |
| ddd4j-cloud-stream | Binding、StreamBridge、ACK/NACK、多 Broker |
| ddd4j-cloud-web | MVC、WebFlux、i18n、异常 |
| ddd4j-cloud-observability | Nacos、Sentinel、monitor、trace、readiness |
| ddd4j-cloud-testing | compatibility、数据库和 Binder 容器 |
| ddd4j-cloud-release | 八线发布和隔离远端消费 |

### Task 1: 版本、架构和 BOM

**Files:** Create skills/ddd4j-cloud-version-selection/、skills/ddd4j-cloud-architecture/、skills/ddd4j-cloud-bom/

- [ ] **Step 1:** 提取八条 Cloud→Boot→ddd4j→JDK/Maven 组合。
- [ ] **Step 2:** 记录来源、SHA、主/备选和验证级别。
- [ ] **Step 3:** 分类上游缺件与 Cloud 自身失败。
- [ ] **Step 4:** 运行矩阵脚本、TRACE 并提交。

### Task 2: context、tenant、Feign

**Files:** Create skills/ddd4j-cloud-context/、skills/ddd4j-cloud-tenant/、skills/ddd4j-cloud-feign/

- [ ] **Step 1:** 追踪过滤器→ThreadContext→异步→Feign 的传播与恢复。
- [ ] **Step 2:** Tenant 覆盖表注解、系统隔离、数据范围和忽略条件。
- [ ] **Step 3:** Feign 覆盖 header、error decoder、重试和清理。
- [ ] **Step 4:** 用异常、线程复用、并发场景验证并提交。

### Task 3: data 与 stream

**Files:** Create skills/ddd4j-cloud-data/、skills/ddd4j-cloud-stream/

- [ ] **Step 1:** Data 统一 datasource、MyBatis/JPA、事务和 Seata。
- [ ] **Step 2:** Stream 解释 function/binding/physical destination 三层命名。
- [ ] **Step 3:** 覆盖 Kafka、RabbitMQ、Pulsar、RocketMQ 的命名和 ACK/NACK。
- [ ] **Step 4:** 使用真实 Broker round-trip 校正并提交。

### Task 4: web 与 observability

**Files:** Create skills/ddd4j-cloud-web/、skills/ddd4j-cloud-observability/

- [ ] **Step 1:** Web 覆盖 MVC/WebFlux、i18n、异常和 context。
- [ ] **Step 2:** Observability 覆盖 Nacos、Sentinel、monitor、trace、readiness。
- [ ] **Step 3:** 区分配置、启动和真实外部服务验收。
- [ ] **Step 4:** 场景验证后提交。

### Task 5: testing 与 release

**Files:** Create skills/ddd4j-cloud-testing/、skills/ddd4j-cloud-release/

- [ ] **Step 1:** Testing 覆盖 compatibility、WebMVC/MySQL、Binder 容器。
- [ ] **Step 2:** Release 覆盖八线串行构建和私服发布。
- [ ] **Step 3:** 隔离缓存消费 parent/BOM/JAR；上游缺件标 BLOCKED。
- [ ] **Step 4:** 更新插件、README、TRACE 和远端 SHA 后提交。
