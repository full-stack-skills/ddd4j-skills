---
name: ddd4j-boot-bom
description: Use when managing ddd4j-boot parent, dependencies, BOM imports, effective POMs, version ownership, Spring Boot dependency alignment, Maven model, or consumer coordinates.
license: Apache-2.0
---

# ddd4j-boot BOM

## Overview

面向当前 ddd4j-boot 维护线的 boot-parent、boot-dependencies、boot-bom、Spring Boot BOM、ddd4j BOM、effective POM。先确认版本线，再应用本技能。

## 核心范围

boot-parent、boot-dependencies、boot-bom、Spring Boot BOM、ddd4j BOM、effective POM。

## 规则

1. 普通第三方版本由 ddd4j-dependencies 治理，Boot 层只覆盖 Boot 生态。
2. BOM 导入顺序必须用 effective POM验证。
3. Boot 4 使用 Maven 4/POM 4.1。
4. 具体模块不得重复固定已管理版本。
5. parent/BOM/聚合 POM是不同职责。

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

