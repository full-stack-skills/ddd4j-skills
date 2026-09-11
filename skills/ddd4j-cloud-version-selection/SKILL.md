---
name: ddd4j-cloud-version-selection
description: Use when choosing a ddd4j-cloud line based on Spring Cloud, Spring Boot, ddd4j, JDK, Maven, POM model, and main versus compatibility pairing constraints.
license: Apache-2.0
---

# ddd4j-cloud 版本选择

## Overview

统一介绍 Hoxton.x、2020.0.x、2021.0.x、2022.0.x、2023.0.x、2024.0.x、2025.0.x、2025.1.x 完整矩阵，不按单个 artifact 拆技能。先选 Cloud→Boot→ddd4j 主组合，再读取当前分支。

## 核心范围

Hoxton.x、2020.0.x、2021.0.x、2022.0.x、2023.0.x、2024.0.x、2025.0.x、2025.1.x 完整矩阵。

## 核心规则

1. 主组合与兼容备选分开，不从分支名猜 Boot/ddd4j。
2. 旧 cmpt 与新 extensions 命名不得混用。
3. Context/Tenant 在同步、异步、Reactor、Feign 终态恢复。
4. Binder、数据库、Nacos、Sentinel 等需真实外部行为证据。
5. 上游缺件、Cloud 失败、CI、发布和消费分别分类。

## 能力边界

### ✅ 擅长

- 版本选择的多实现选择与 Spring Cloud 集成。
- 上下游版本和跨服务边界。
- 八维护线差异。

### ⚠️ 需要素材

- 目标 Cloud 线、Boot parent 和 POM。
- 功能、外部服务与部署要求。
- 当前源码/测试/远端证据。

### ❌ 超范围

- 把 README 模块名当功能完成。
- 用配置存在替代外部服务行为。
- 未授权发布或生产操作。

## 工作流

1. 选择主版本组合。
2. 定位 extension、入口和上下游依赖。
3. 比较实现、传播、降级和生命周期。
4. 读取适当合同/验证 consumer 证据。
5. 输出版本、实现、外部依赖和风险。

## 输出与异常

缺少时输出“缺少：Cloud 线/上游/外部服务；补充方式：提供 POM 和验收行为”。

## 深度参考

- [功能矩阵](references/feature-matrix.md)
- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出 Nacos/Redis/Broker/数据库/私服凭据或真实租户数据。

## 快速开始

- “使用 `$ddd4j-cloud-version-selection` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-cloud-version-selection` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-cloud-version-selection` 给出实现选择、证据状态和剩余风险。”

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
