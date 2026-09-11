---
name: ddd4j-jackson
description: Use when working with current ddd4j Jackson 3 JSON utilities, domain-event payload serialization, Jackson 2 annotation compatibility, cache serialization, or Javalin Jackson 3 integration; not for legacy JacksonKit/Sensitive conventions.
license: Apache-2.0
---

# ddd4j Jackson

## Overview

指导当前 ddd4j 的 Jackson 3 数据绑定与事件载荷安全序列化。3.0.x 使用 `tools.jackson.databind`，同时保留 `com.fasterxml.jackson.annotation` 2.22 注解兼容层。

## 快速开始

- “用 JsonKit 序列化 ddd4j 对象。”
- “为 EventStore 配置 EventPayloadSerializer。”
- “排查 JavalinJackson3 的 JsonApplyView 缺类。”
- “审查缓存 ObjectMapper 是否安全。”

## 受众、路由与定制

- 事件存储开发者：指定事件类型、存储适配器和安全策略。
- Web/缓存开发者：指定 HTTP、Redis 或其他缓存边界。
- 依赖维护者：指定维护线、databind/annotations 版本与目标运行时。
- 纯通用 Jackson 问题：转用 Jackson 技能，不引入 ddd4j 假设。

输入不足时先按当前检出给出暂定代际判断，再列出“缺少：mapper 场景/依赖树/维护线；补充方式：提供 POM 或 dependency tree”。

## 能力边界

### ✅ 擅长

1. `io.ddd4j.kit.lang.JsonKit` 的 JSON、类型转换和日期格式。
2. `EventPayloadSerializer` 的领域事件 payload 白名单序列化。
3. Jackson 3 databind 与 Jackson 2 annotations 的双代际边界。
4. Javalin、缓存和事件存储中的 ObjectMapper 使用。

### ⚠️ 需要素材

1. 当前维护线；2.0.x 与 3.0.x Jackson 行为不同。
2. 目标是 HTTP、缓存还是 EventStore。
3. 允许反序列化的事件类型集合和安全策略。

### ❌ 超范围

1. 不存在于当前源码的 `JacksonKit`、`ToLongDeserializer`、`SensitiveStrategy`。
2. 将 Web ObjectMapper、缓存 mapper、事件 mapper 混成一个全局实例。
3. 通用 Jackson 教程或 Boot 自动配置。

## 快速参考

| 场景 | 当前做法 |
|---|---|
| 通用工具 | `JsonKit` |
| 事件载荷 | `EventPayloadSerializer` + 隔离后的 mapper |
| Jackson 3 databind | `tools.jackson.*` |
| 兼容注解 | `com.fasterxml.jackson.annotation.*` 2.22 |
| Javalin 7 | `JavalinJackson3` |
| 日期 | `JsonKit.DATE_PATTERN/TIME_PATTERN` 对应 formatter |
| 多态 | 事件序列化禁止依赖 `@class`/默认类型激活 |
| Redis | `JsonKit.REDIS_OBJECT_MAPPER` 当前启用 DefaultTyping，只能处理受信任缓存数据，不能用于外部事件 payload |

## 示例

```java
JsonMapper mapper = JsonMapper.builder()
        .findAndAddModules()
        .build();

EventPayloadSerializer serializer = new EventPayloadSerializer(mapper);
String payload = serializer.serialize(event);
OrderPaid restored = serializer.deserialize(payload, OrderPaid.class);
```

必须由调用方提供已验证的事件类型，不能根据不可信 payload 任意加载类。

## 工作流

1. 先确认维护线、依赖树和实际 `ObjectMapper` 类型。
2. 区分 HTTP、缓存、事件存储三种序列化边界。
3. 对事件执行成功 round-trip、未知字段、损坏 payload 和非法类型测试。
4. 对 Javalin 7 同时检查 Jackson 3 databind 与 annotations 2.22。
5. 修改 BOM 后用 effective POM 和运行测试验证，不能只看声明版本。

## 常见错误

- 导入 `com.fasterxml.jackson.databind.ObjectMapper` 到 3.0.x。
- 继续调用旧 `JacksonKit`。
- 为事件开启 unrestricted default typing。
- 在领域响应上暴露内部聚合结构。
- annotations 被上游 BOM 压低后，把 `JsonApplyView` 缺类误诊为业务错误。
- 用热缓存掩盖远端依赖版本错误。

## 输出与异常

明确列出 databind、annotations、使用场景和维护线。缺失时输出“缺少：Jackson 代际或 mapper 来源；补充方式：提供 dependency tree/effective POM”。

## 隐私与安全

反序列化不可信 JSON 时使用明确类型和允许列表；日志不得打印 Token、敏感 payload 或私服凭据。

## FAQ

1. **为何同时出现 tools.jackson 与 com.fasterxml 注解？** Jackson 3 databind 兼容独立的 2.x annotations 包。
2. **JsonKit 等于全局 Web mapper 吗？** 不等于。
3. **事件能启用 default typing 吗？** 当前安全契约不依赖它。
4. **Javalin 7 必须 Jackson 3 吗？** 以当前模块 POM和测试为准，现行样例使用 JavalinJackson3。
5. **日期一定是 ISO 吗？** `JsonKit` 有自己的 formatter；具体 HTTP 契约需看适配器。
6. **怎样证明兼容？** 依赖树、round-trip、损坏输入和运行时集成测试共同证明。

## 深度参考

- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)
