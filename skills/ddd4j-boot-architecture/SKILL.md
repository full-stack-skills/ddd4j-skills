---
name: ddd4j-boot-architecture
description: Use when designing or reviewing ddd4j-boot module boundaries, parent/BOM layering, Spring Boot integration responsibilities, starter aggregation, or dependencies between core, auth, data, MQ, Web, cache, and extensions.
license: Apache-2.0
---

# ddd4j-boot 架构

## Overview

面向当前 ddd4j-boot 维护线的 parent、dependencies、bom、core、auth、data、mq、web、cache、extensions、samples。先确认版本线，再应用本技能。

## 核心范围

parent、dependencies、bom、core、auth、data、mq、web、cache、extensions、samples。

## 规则

1. Boot 层只装配 ddd4j 能力，不复制 core 实现。
2. 聚合 POM 与具体实现模块分离。
3. 条件装配和生命周期属于具体功能模块。
4. 跨维护线保留各自 JDK/Maven/POM。
5. 模块存在不等于自动配置已生效。

## 能力边界

### ✅ 擅长

- 当前 Boot 专有架构和配置决策。
- 多实现选择与职责划分。
- 维护线差异和验证路径。

### ⚠️ 需要素材

- 目标 Boot 线、JDK、Maven 和 POM。
- 目标模块和运行行为。
- 当前源码/测试/CI 状态。

### ❌ 超范围

- 改写 ddd4j core 领域契约。
- 把依赖存在当运行时成功。
- 自动发布或升级生产项目。

## 工作流

1. 运行 ddd4j-boot-version-selection。
2. 读取目标线 POM、源码、AutoConfiguration 和测试。
3. 比较候选实现并明确默认/覆盖/降级。
4. 执行目标上下文或行为测试。
5. 分别报告源码、测试、CI 和发布证据。

## 输出与异常

输出版本线、模块、配置入口、默认实现、覆盖点、测试和风险。缺少时写“缺少：目标线或模块；补充方式：提供 POM 和行为要求”。

## 深度参考

- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出 settings、Token、密码或生产连接信息。

