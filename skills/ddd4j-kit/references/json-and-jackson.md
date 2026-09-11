# JSON 与 Jackson

## 当前入口

- io.ddd4j.kit.lang.JsonKit
- JsonKit.DEFAULT_OBJECT_MAPPER
- JsonKit.REDIS_OBJECT_MAPPER
- io.ddd4j.core.cqrs.eventstore.jackson.EventPayloadSerializer

## 场景选择

| 场景 | 选择 |
|---|---|
| 普通对象 JSON | JsonKit 默认 mapper/API |
| Redis 受信任对象 | REDIS_OBJECT_MAPPER |
| EventStore payload | EventPayloadSerializer + 显式事件 Class |
| Javalin 7 HTTP | 对应 JavalinJackson3 配置 |

Redis mapper 的 DefaultTyping 不能用于不可信外部数据。事件 payload 禁止依赖 @class。
