---
name: ddd4j-metrics
description: Use when instrumenting or reviewing ddd4j projection, runtime, Web, MQ, cache, or domain-operation metrics, especially OpenTelemetry counters, timers, failures, labels, and observability evidence.
license: Apache-2.0
---

# ddd4j Metrics

## Overview

指标必须描述可观察行为并保持低基数；当前专有实现以 ProjectionMetrics 和 OpenTelemetryProjectionMetrics 为核心，其他能力按真实 adapter 扩展。

## 核心规则

1. 端口定义在核心能力，OpenTelemetry 位于 metrics/extension adapter。
2. success/failure、duration、processed count 分开。
3. tenant/user/message id 不作为高基数 label。
4. Noop 实现是降级，不是观测成功。
5. 指标测试验证名称、标签、递增和异常路径。
6. 指标不能替代日志、trace、readiness 或业务验收。

## 能力边界

### ✅ 擅长

- ProjectionMetrics/OpenTelemetry。
- Web/MQ/Cache/Runtime 指标设计。
- label 基数和隐私审查。
- 指标测试与证据分级。

### ⚠️ 需要素材

- 观测后端和命名规范。
- SLI/SLO 和告警目标。
- 目标模块当前 instrumentation。

### ❌ 超范围

- 编造不存在的指标。
- PII 作为标签。
- 指标存在即生产可观测。

## 深度参考

- [Projection 指标](references/projection.md)
- [跨能力指标](references/cross-capability.md)
- [测试与告警](references/testing-and-alerting.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

标签不得包含 Token、用户 ID、手机号、完整 URL、SQL 或消息体。

## 快速开始

- “使用 `$ddd4j-metrics` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-metrics` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-metrics` 给出实现选择、证据状态和剩余风险。”

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
