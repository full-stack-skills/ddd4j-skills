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

## 快速开始

- “使用 `$ddd4j-boot-bom` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-boot-bom` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-boot-bom` 给出实现选择、证据状态和剩余风险。”

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
