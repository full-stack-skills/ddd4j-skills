---
name: ddd4j-quarkus-cache
description: Use when integrating Quarkus Cache, Redis, or ddd4j Cache SPI with Quarkus, including TTL, CAS, idempotency, bean scopes, and lifecycle.
license: Apache-2.0
---

# ddd4j-quarkus 缓存

## Overview

统一介绍 Quarkus Cache、Redis、ddd4j Cache SPI、TTL、CAS、幂等、CDI scope，不按 artifact 拆技能。先选择 3.3.x 或 4.0.x，再读取当前源码。

## 核心范围

Quarkus Cache、Redis、ddd4j Cache SPI、TTL、CAS、幂等、CDI scope。

## 核心规则

1. 3.3.x 与 4.0.x 分别保留 ddd4j/JDK/Maven/POM/Quarkus 契约。
2. 4.0.x 是适配器线名，不代表 Quarkus Platform 4。
3. CDI/Arc、runtime/deployment、BuildItem/Recorder 不用 Spring 模型解释。
4. Bean scope、请求 Context、启动/关闭和 native 边界明确。
5. 源码、测试、CI、Security、发布分层报告。

## 能力边界

### ✅ 擅长

- 缓存的多实现选择与 Quarkus 适配。
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

## 快速开始

- “使用 `$ddd4j-quarkus-cache` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-quarkus-cache` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-quarkus-cache` 给出实现选择、证据状态和剩余风险。”

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
