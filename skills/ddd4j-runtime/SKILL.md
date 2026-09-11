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

