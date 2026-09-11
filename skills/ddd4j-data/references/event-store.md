# EventStore

端口：EventStore/AsyncEventStore、StoredEvent、AggregateVersionConflictException。

实现：JDBI、JPA、R2DBC、Panache、EventStoreDB。append 必须校验 expected version，多事件批次原子写；序列化使用显式事件类型。测试覆盖冲突、回滚、并发、顺序和损坏 payload。
