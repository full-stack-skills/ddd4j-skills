---
name: ddd4j-web
description: Use when implementing or reviewing ddd4j HTTP contracts across Spring MVC, WebFlux, Javalin, Quarkus REST, Micronaut, Vert.x, Helidon, or Dropwizard, including context, errors, validation, authentication, idempotency, CORS, limits, and readiness.
license: Apache-2.0
---

# ddd4j Web

## Overview

ddd4j-web-core 定义跨运行时行为，各适配器实现同一 HTTP 契约；框架 API 可以不同，响应、上下文和安全行为必须一致。

## 运行时与能力

Spring MVC、WebFlux、Javalin、Quarkus REST、Micronaut、Vert.x、Helidon、Dropwizard；统一覆盖响应/错误、Request/Trace/Tenant Context、认证、幂等、CORS、request size、async timeout、liveness/readiness 和 Validation。

## 核心规则

1. 请求开始绑定上下文，成功/异常/异步结束都清理。
2. 认证失败、授权失败、验证失败和系统错误使用稳定状态码/载荷。
3. 幂等区分关闭、本地单实例和共享 CAS。
4. CORS 生产使用明确 allowlist。
5. liveness 与 readiness 分离，readiness 聚合真实依赖。
6. Testkit contract 是跨运行时对齐证据。

## 能力边界

### ✅ 擅长

- 多 Web 运行时统一契约。
- Context、错误、认证、幂等、CORS、Readiness。
- Validation 四个 ddd4j 约束。
- HTTP contract 测试。

### ⚠️ 需要素材

- 目标运行时/维护线。
- 公开端点和错误契约。
- 部署、代理和认证模式。

### ❌ 超范围

- 用 HTTP 200 证明业务正确。
- 固定 READY。
- 把框架 Context 泄漏进领域层。

## 工作流

1. 选择运行时并读取对应 adapter。
2. 以 web-testkit 路径/载荷定义行为。
3. 实现绑定、认证、处理、异常和清理。
4. 配置 CORS/limits/idempotency/readiness。
5. 执行正常、错误、重复请求和同线程复用测试。

## 深度参考

- [运行时矩阵](references/runtime-matrix.md)
- [上下文与错误](references/context-and-errors.md)
- [Validation](references/validation.md)
- [幂等、CORS、Readiness](references/production-controls.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得记录 Authorization、Cookie、完整请求体或隐私字段。

## 快速开始

- “使用 `$ddd4j-web` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-web` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-web` 给出实现选择、证据状态和剩余风险。”

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
