# 反模式

1. **旧 CRUD 基类冒充核心**：使用 `io.hiwepy.boot BaseEntity`；改为从当前 `AggregateRoot/Repository` 建模。
2. **混合持久化轨道**：同一聚合既 `save()` 又持久化 `pullDomainEvents()`；选择单一策略。
3. **领域依赖框架**：Domain 导入 Spring/MyBatis/Javalin；通过 core SPI 隔离。
4. **上下文泄漏**：绑定 Subject 后未关闭；使用作用域/finally。
5. **默认方法假绿**：未覆盖 Repository 操作却认为可用；测试实际适配器并处理 UnsupportedOperationException。
