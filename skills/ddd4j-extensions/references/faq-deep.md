# 深度 FAQ

1. **Jackson 是独立 extension 吗？** 当前核心能力在 kit/core。
2. **Akka 在哪里？** 当前主要在 Boot 扩展。
3. **PF4J 插件可信么？** 需来源和权限策略。
4. **QLExpress 能执行任意代码吗？** 按 builder 权限和函数 allowlist 限制。
5. **License 能绕过吗？** 不能。
6. **OTel 等于 metrics 模块吗？** 是适配/导出关系，不同职责。
7. **扩展关闭会影响 core 吗？** 应可选降级。
8. **配置开关谁实现？** 具体 runtime/auto-configuration。
9. **扩展需要 BOM 吗？** 由 ddd4j-bom 管理消费版本。
10. **完成证据是什么？** 模块测试、运行时装配和外部行为。
