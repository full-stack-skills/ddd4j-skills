---
name: ddd4j-javalin-web
description: Use when building ddd4j-javalin routes, request context, errors, CORS, authentication, validation, idempotency, request limits, async timeouts, or health endpoints.
license: Apache-2.0
---

# ddd4j-javalin Web

## Overview

统一介绍 routes、Request/Trace/Tenant Context、errors、CORS、auth、validation、idempotency、limits、async、health。先用 ddd4j-javalin-version-selection 确认维护线，再读取当前分支源码。

## 核心范围

routes、Request/Trace/Tenant Context、errors、CORS、auth、validation、idempotency、limits、async、health。

## 核心规则

1. 6.7.x、7.1.x、7.2.x 分别保留 Javalin/JDK/Maven/POM 契约。
2. Javalin 6 与 7 API 差异按行为对齐，不机械复制。
3. 配置、启动、HTTP、容器、CI、发布分层报告。
4. Context/Subject/资源在成功、异常和异步终态清理。
5. 生产依赖需真实 readiness、共享 CAS、明确 CORS 和幂等关闭。

## 能力边界

### ✅ 擅长

- Web的多实现选择和 Javalin 适配。
- 生命周期、配置和行为边界。
- 三维护线差异。

### ⚠️ 需要素材

- 目标分支、POM和 Javalin 版本。
- 业务行为、依赖和部署模式。
- 当前源码/测试/CI 证据。

### ❌ 超范围

- 把 Javalin 6 代码直接复制到 7。
- 用 smoke test 代替真实行为。
- 未授权发布或生产变更。

## 工作流

1. 选择版本线。
2. 定位功能模块、入口和 provider。
3. 比较实现、配置、覆盖和降级。
4. 读取/执行适当合同证据。
5. 输出版本、行为、生命周期和风险。

## 输出与异常

缺少时输出“缺少：目标线/实现/配置；补充方式：提供 POM 和验收行为”，并继续安全只读检查。

## 深度参考

- [功能矩阵](references/feature-matrix.md)
- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出 Token、Cookie、OIDC secret、数据库或私服凭据。

## 快速开始

- “使用 `$ddd4j-javalin-web` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-javalin-web` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-javalin-web` 给出实现选择、证据状态和剩余风险。”

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
