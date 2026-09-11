# 深度 FAQ

1. **JsonKit 是否线程安全？** 依据其静态 mapper 与当前实现核验，不自行替换配置。
2. **Jackson 3 为何还用 com.fasterxml 注解？** annotations 包保持兼容。
3. **findAndAddModules 是否总需要？** 按当前 mapper 场景和测试决定。
4. **事件 payload 能存类名吗？** 当前硬化契约不依赖 @class。
5. **未知字段如何处理？** Jackson 2/3 默认不同，必须逐线测试。
6. **ZonedDateTime 如何断言？** 数字时间戳可能丢 ZoneId，按 instant 契约测试。
7. **缓存为何单独 mapper？** 生命周期、安全和类型需求与 HTTP 不同。
8. **JsonApplyView 缺失怎么查？** 对齐 databind 与 annotations 版本。
9. **能覆盖全局日期格式吗？** 只在明确的 HTTP/工具契约内，避免破坏事件回放。
10. **如何验证私服版本？** 用隔离 Maven 缓存消费并检查依赖树。
