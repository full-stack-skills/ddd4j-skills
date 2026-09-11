---
name: ddd4j-architecture
description: Use when designing, reviewing, or locating boundaries in ddd4j modules, DDD/CQRS layers, ports and adapters, runtime integrations, or dependency direction.
license: Apache-2.0
---

# ddd4j 架构

## Overview

ddd4j 的稳定中心是框架无关的领域/CQRS/SPI，外围模块提供数据、消息、Web、认证、缓存、观测和运行时适配。

## 快速开始

- “领域层能否依赖 MyBatis Wrapper？”
- “CommandBus 应该在哪个模块装配？”
- “新增 Broker 应实现 core 还是 mq 模块？”
- “Spring、Guice、Quarkus CDI 如何共享核心契约？”

## 架构分区

| 分区 | 职责 |
|---|---|
| annotation | DDD/CQRS/API/ORM 元数据 |
| core | AggregateRoot、Command/Query、Event、Repository、Context、SPI |
| kit | 基础工具，不承载业务运行时 |
| auth/data/mq/web/cache/metrics | 能力接口实现与聚合 |
| runtime-* | Spring、Guice、Quarkus 等 DI 和生命周期绑定 |
| extensions | 跨领域可选扩展 |
| ddd-rules | 架构约束和静态检查 |
| parent/dependencies/bom | 构建、版本所有权和消费面 |

## 决策规则

1. Domain 只依赖 core/annotation/必要值类型。
2. ORM、Broker、HTTP、认证框架位于适配层。
3. 静态门面通过 Contexts/Registry/SPI 解析实现。
4. 框架运行时负责注册、请求作用域、回滚和关闭。
5. BOM 只管理版本，不证明运行时实现已装配。
6. 同一聚合不得混用快照 Active Record 与 Event Sourcing。

## 能力边界

### ✅ 擅长

- 模块归属和依赖方向。
- DDD/CQRS 与端口适配。
- 多运行时共享核心。
- 架构审查和新能力落位。

### ⚠️ 需要素材

- 目标维护线和模块 POM。
- 业务行为与事务边界。
- 运行时和部署模型。

### ❌ 超范围

- 具体框架 API 详解。
- 仅凭目录名判断实现完成。
- 未验证的跨维护线等价声明。

## 工作流

1. 确认 Git 根、分支和 CodeGraph 健康。
2. 从调用链找核心端口和实际适配器。
3. 标出编译依赖、运行时注册和资源生命周期。
4. 用架构测试、行为测试和运行证据分别验证。
5. 输出事实、推断、违规项和建议落位。

## 常见错误

- Domain 导入 Spring/MyBatis/Javalin/Quarkus 类型。
- 在 core 创建具体 Broker/数据库客户端。
- 把 runtime 注册遗漏误诊为 core API 缺失。
- 聚合模块名称被当作功能证据。
- 只看依赖树不看调用和生命周期。

## 输出与异常

输出“当前分支、模块、端口、适配器、注册点、测试、风险”。找不到实现时写“缺少：具体适配器/注册点；补充方式：提供模块或运行时”，不得补写虚构链路。

## 深度参考

- [模块边界](references/module-boundaries.md)
- [依赖规则](references/dependency-rules.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

架构证据不得包含凭据、真实租户数据或私服认证信息。

