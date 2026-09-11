# 源码证据索引

以用户指定的当前检出为准，历史路径仅用于定位：

- `ddd4j-core/.../ddd/model/AggregateRoot.java`：Active Record/Event Sourcing 双模式及禁止混用。
- `ddd4j-core/.../cqrs/command/{Command,CommandBus,Result}.java`：写侧。
- `ddd4j-core/.../cqrs/query/{Query,PersistenceQueryScope}.java`：领域查询与 PO 作用域。
- `ddd4j-core/.../ddd/repository/{Repository,RepositoryRegistry}.java`：ORM 无关仓储。
- `ddd4j-core/.../ddd/event/DomainEvent.java`：事件元数据、发布与回放。
- `ddd4j-core/.../context/{Contexts,ThreadContext}.java`：SPI 与上下文。
- `ddd4j-core/src/test/java/io/ddd4j/core/arch/CoreIndependenceTest.java`：核心依赖边界。

每次使用时重新读取当前分支；不要把 3.0.x 的 Java/Jackson/API 语义直接移植到旧线。
