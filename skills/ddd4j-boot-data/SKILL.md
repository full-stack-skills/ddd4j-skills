---
name: ddd4j-boot-data
description: Use when integrating ddd4j data capabilities in Spring Boot with JDBC, JPA, MyBatis, MyBatis-Plus, database migrations, transactions, repositories, projections, or Outbox.
license: Apache-2.0
---

# ddd4j-boot 数据

## Overview

统一介绍 JDBC、JPA、MyBatis、MyBatis-Plus、Flyway、事务、Repository、Projection、Outbox，不按单个 artifact 拆技能。使用前先通过 ddd4j-boot-version-selection 确认维护线。

## 核心范围

JDBC、JPA、MyBatis、MyBatis-Plus、Flyway、事务、Repository、Projection、Outbox。

## 核心规则

1. 从当前目标线 POM、源码和测试取证。
2. 默认实现允许用户显式覆盖，关闭开关必须真正不装配。
3. 配置存在、Bean 创建、行为测试、CI 和发布分别报告。
4. 资源必须明确 owner、失败回滚和幂等关闭。
5. Boot 2/3/4 的 API、JDK、Maven 差异逐线处理。

## 能力边界

### ✅ 擅长

- 数据的多实现选择与 Spring Boot 装配。
- 配置、覆盖、生命周期和验证。
- 维护线兼容性判断。

### ⚠️ 需要素材

- 目标 Boot 线、POM和配置。
- 业务行为、依赖和部署模式。
- 当前测试/CI/运行证据。

### ❌ 超范围

- 修改 ddd4j core 公共语义。
- 用依赖或 Bean 存在替代真实行为。
- 未授权发布或生产操作。

## 工作流

1. 选择版本线。
2. 定位该功能的聚合和具体实现。
3. 比较实现、默认值、覆盖和降级。
4. 执行目标上下文及行为测试。
5. 输出版本、配置、生命周期、证据和风险。

## 输出与异常

缺少信息时输出“缺少：目标线/实现/配置；补充方式：提供 POM 和验收行为”，并继续安全只读检查。

## 深度参考

- [功能矩阵](references/feature-matrix.md)
- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出凭据、Token、生产连接串或敏感业务数据。

