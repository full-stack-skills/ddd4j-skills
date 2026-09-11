---
name: ddd4j-runtime
description: Use when integrating or reviewing ddd4j runtime bindings for Spring, Guice, Quarkus CDI, Micronaut, Vert.x, Helidon, or Dropwizard, including SPI registration, context, buses, publishers, readiness, startup rollback, and shutdown.
license: Apache-2.0
---

# ddd4j Runtime

## Overview

Runtime 把框架容器绑定到 ddd4j core 端口；核心不依赖 DI 框架，运行时负责唯一注册、请求作用域和资源生命周期。

## 运行时

Spring、Guice、Quarkus CDI、Micronaut、Vert.x、Helidon、Dropwizard，以及 runtime-testkit。

## 统一职责

- 注册 CommandBus、DomainEventPublisher、SubjectProvider、Cache/Repository 等 SPI。
- 建立 Request/Thread/Reactive Context。
- 初始化依赖并汇总 readiness。
- 部分失败时逆序回滚。
- drain 后幂等 close。
- 防止重复注册和 shutdown hook 泄漏。

## 能力边界

### ✅ 擅长

- DI/SPI 装配。
- Context 与 Subject 生命周期。
- Startup/readiness/drain/close。
- 多运行时行为对齐。

### ⚠️ 需要素材

- 目标运行时与维护线。
- 需要注册的 SPI。
- 资源依赖和关闭顺序。

### ❌ 超范围

- 把 Spring 注解用于所有运行时。
- 重复注册后任意覆盖。
- 只启动容器就称运行时 ready。

## 工作流

1. 列出端口和 provider。
2. 定义依赖顺序。
3. 注册并检测重复。
4. 绑定/恢复请求上下文。
5. 聚合 readiness。
6. 逆序回滚、drain、close。
7. 用 runtime-testkit 和目标框架测试。

## 深度参考

- [运行时矩阵](references/runtime-matrix.md)
- [SPI 注册](references/spi-registration.md)
- [生命周期](references/lifecycle.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

Context 不得跨请求泄漏 Subject、Tenant 或 Token。

## 快速开始

- “使用 `$ddd4j-runtime` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-runtime` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-runtime` 给出实现选择、证据状态和剩余风险。”

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
