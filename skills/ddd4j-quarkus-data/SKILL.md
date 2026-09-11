---
name: ddd4j-quarkus-data
description: Use when integrating Panache, JPA, JDBI, R2DBC, repositories, composite keys, tenants, transactions, EventStore, Projection, or Outbox with ddd4j-quarkus.
license: Apache-2.0
---

# ddd4j-quarkus 数据

## Overview

统一介绍 Panache、JPA、JDBI、R2DBC、Repository、复合键、租户、事务、EventStore、Projection、Outbox，不按 artifact 拆技能。先选择 3.3.x 或 4.0.x，再读取当前源码。

## 核心范围

Panache、JPA、JDBI、R2DBC、Repository、复合键、租户、事务、EventStore、Projection、Outbox。

## 核心规则

1. 3.3.x 与 4.0.x 分别保留 ddd4j/JDK/Maven/POM/Quarkus 契约。
2. 4.0.x 是适配器线名，不代表 Quarkus Platform 4。
3. CDI/Arc、runtime/deployment、BuildItem/Recorder 不用 Spring 模型解释。
4. Bean scope、请求 Context、启动/关闭和 native 边界明确。
5. 源码、测试、CI、Security、发布分层报告。

## 能力边界

### ✅ 擅长

- 数据的多实现选择与 Quarkus 适配。
- CDI、构建期和运行期边界。
- 双维护线差异。

### ⚠️ 需要素材

- 目标线、POM和 Quarkus Platform。
- 功能、运行时和部署要求。
- 当前源码/测试/CI 证据。

### ❌ 超范围

- 用 Spring 装配模型替代 Quarkus。
- 把 BOM 引入当 Bean 已注册。
- 未授权发布或生产变更。

## 工作流

1. 选择版本线。
2. 定位 runtime/deployment 或功能模块。
3. 核对 CDI scope、配置和生命周期。
4. 读取适当 Arc/QuarkusTest/合同证据。
5. 输出版本、实现、证据和风险。

## 输出与异常

缺少时输出“缺少：目标线/扩展/运行时；补充方式：提供 POM 和验收行为”。

## 深度参考

- [功能矩阵](references/feature-matrix.md)
- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出 Token、OIDC secret、数据库、Broker 或私服凭据。

