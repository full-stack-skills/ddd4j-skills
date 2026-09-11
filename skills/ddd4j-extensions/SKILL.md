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

