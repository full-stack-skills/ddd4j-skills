---
name: ddd4j-javalin-architecture
description: Use when designing or reviewing ddd4j-javalin module boundaries, parent/BOM layering, runtime composition, auth, data, MQ, Web, cache, extensions, testcontainers, or samples.
license: Apache-2.0
---

# ddd4j-javalin 架构

## Overview

统一介绍 parent、bom、dependencies、core、ddd、auth、data、mq、web、cache、extensions、testcontainers。先用 ddd4j-javalin-version-selection 确认维护线，再读取当前分支源码。

## 核心范围

parent、bom、dependencies、core、ddd、auth、data、mq、web、cache、extensions、testcontainers。

## 核心规则

1. 6.7.x、7.1.x、7.2.x 分别保留 Javalin/JDK/Maven/POM 契约。
2. Javalin 6 与 7 API 差异按行为对齐，不机械复制。
3. 配置、启动、HTTP、容器、CI、发布分层报告。
4. Context/Subject/资源在成功、异常和异步终态清理。
5. 生产依赖需真实 readiness、共享 CAS、明确 CORS 和幂等关闭。

## 能力边界

### ✅ 擅长

- 架构的多实现选择和 Javalin 适配。
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

