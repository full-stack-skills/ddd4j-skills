---
name: ddd4j-extensions
description: Use when choosing, integrating, or reviewing optional ddd4j extensions such as Excel, license, monitoring, OpenTelemetry, PF4J, QLExpress, QR code, validation, or Jackson-related integration boundaries.
license: Apache-2.0
---

# ddd4j Extensions

## Overview

扩展是可选能力，不应反向污染 core。当前 3.0.x 顶层 extensions 包含 Excel、License、Monitor、OTel、PF4J、QLExpress、QRCode、Validation；Jackson 核心工具在 ddd4j-kit/core，Akka 当前主要在 ddd4j-boot。

## 选择矩阵

| 需求 | 扩展 |
|---|---|
| Excel | extension-excel |
| 许可证 | extension-license |
| 日志/告警配置 | extension-monitor |
| Trace/metrics | extension-otel |
| 插件系统 | extension-pf4j |
| 规则表达式 | extension-qlexpress |
| 二维码 | extension-qrcode |
| 扩展校验 | extension-validation |

## 核心规则

1. classpath 缺失时不影响 core。
2. 扩展提供框架无关能力，Boot/Quarkus 等负责装配。
3. 配置开关、默认实现、用户覆盖和 close 明确。
4. 不把历史/Boot 专有扩展写成当前 core 模块。
5. 每项用当前模块和测试证明。

## 能力边界

### ✅ 擅长

- 扩展选择和集成。
- core/extension/runtime 边界。
- 可选依赖和生命周期。
- 扩展测试与降级。

### ⚠️ 需要素材

- 当前维护线和目标运行时。
- 目标扩展与配置。
- 外部服务/许可证要求。

### ❌ 超范围

- 模块不存在却宣称支持。
- 扩展依赖泄漏 core。
- 许可证校验绕过。

## 深度参考

- [当前扩展](references/current-extensions.md)
- [集成模式](references/integration-pattern.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

License、监控、插件和表达式输入可能敏感；不得记录密钥，规则/插件需沙箱和允许列表。

## 快速开始

- “使用 `$ddd4j-extensions` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-extensions` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-extensions` 给出实现选择、证据状态和剩余风险。”

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
