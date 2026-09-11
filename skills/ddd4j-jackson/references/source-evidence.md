# 源码证据索引

- `ddd4j-kit/.../JsonKit.java`：合并后的 JSON/Jackson 工具、日期 formatter、类型转换。
- `ddd4j-core/.../cqrs/eventstore/jackson/EventPayloadSerializer.java`：Jackson 3 安全事件载荷。
- `ddd4j-core/.../ddd/event/DomainEvent.java`：注解与无参回放契约。
- `ddd4j-core/pom.xml`：`tools.jackson.databind` 与 `com.fasterxml.jackson.annotation` 并存原因。
- `ddd4j-dependencies/pom.xml`：databind/annotations 版本管理。
- `ddd4j-samples/ddd4j-sample-javalin*/pom.xml`：JavalinJackson3 与 JsonApplyView 风险。
- `ddd4j-cache/*Cache.java`：缓存 mapper 的独立使用边界。

修改后至少运行 EventPayloadSerializer、DomainEvent round-trip 和目标适配器测试。
