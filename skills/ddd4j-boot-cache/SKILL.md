---
name: ddd4j-boot-cache
description: Use when configuring ddd4j caches in Spring Boot with local providers, Redis, Redisson, JetCache, TTL, CAS, idempotency, and readiness behavior.
license: Apache-2.0
---

# ddd4j-boot 缓存

## Overview

统一介绍 Caffeine/Guava/Hutool、Redis、Redisson、JetCache、TTL、CAS、幂等，不按单个 artifact 拆技能。使用前先通过 ddd4j-boot-version-selection 确认维护线。

## 核心范围

Caffeine/Guava/Hutool、Redis、Redisson、JetCache、TTL、CAS、幂等。

## 核心规则

1. 从当前目标线 POM、源码和测试取证。
2. 默认实现允许用户显式覆盖，关闭开关必须真正不装配。
3. 配置存在、Bean 创建、行为测试、CI 和发布分别报告。
4. 资源必须明确 owner、失败回滚和幂等关闭。
5. Boot 2/3/4 的 API、JDK、Maven 差异逐线处理。

## 能力边界

### ✅ 擅长

- 缓存的多实现选择与 Spring Boot 装配。
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

## 快速开始

- “使用 `$ddd4j-boot-cache` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-boot-cache` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-boot-cache` 给出实现选择、证据状态和剩余风险。”

## 受众与定制

- 开发者：提供目标维护线、POM、功能和验收行为。
- 架构师：指定只读边界审查、兼容性或迁移目标。
- 测试/发布人员：指定所需证据层级，不自动扩大到发布或生产操作。

可定制目标框架、允许实现、排除模块、兼容性要求和输出证据层级。输入不足时先给暂定判断，再列出“缺少：具体项；补充方式：所需路径或配置”。

## 常见问题

1. **是否按 Maven artifact 创建技能？** 不，按用户面对的功能域组织。
2. **是否能直接套用其他维护线？** 不能，先核对版本和源码。
3. **源码中有类就表示能力可用吗？** 不表示，还需注册和行为证据。
4. **测试未运行如何报告？** 标记 NOT RUN 或 BLOCKED。
5. **可以自动提交或发布吗？** 只有用户明确授权后才执行。
6. **找不到实现怎么办？** 说明缺失的模块或证据，不编造 API。
