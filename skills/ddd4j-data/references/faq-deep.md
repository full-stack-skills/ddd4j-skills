# 深度 FAQ

1. **快照和事件溯源能混用吗？** 同一聚合不应混用。
2. **JPA Entity 是 AggregateRoot 吗？** 建议分离，除非明确权衡。
3. **原生 MyBatis 支持删除吗？** 默认 mapper 不定义，需显式实现。
4. **R2DBC 能加入阻塞事务吗？** 不能假定。
5. **Panache 只用于 Quarkus 吗？** 是对应运行时适配。
6. **Projection 一定实时吗？** 不一定，需定义延迟和恢复。
7. **Outbox 等于 MQ 吗？** 不等于，是可靠发布存储模式。
8. **EventStore append 如何并发？** expected version/数据库约束。
9. **租户忽略何时允许？** 受控系统操作并审计。
10. **完成证据是什么？** 真实数据库、事务、并发、恢复测试。

