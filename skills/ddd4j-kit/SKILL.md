---
name: ddd4j-kit
description: Use when selecting or applying current ddd4j utility APIs for JSON, bean mapping, strings, collections, identifiers, functions, dates, arrays, reflection, or low-level reusable helpers.
license: Apache-2.0
---

# ddd4j Kit

## Overview

优先使用 ddd4j 已提供的稳定工具，避免在业务模块重复封装；先确认工具的 null、异常、类型和线程安全语义。

## 路由

| 需求 | 工具族 |
|---|---|
| JSON/Jackson、类型转换 | JsonKit |
| Bean 属性和映射 | BeanKit、MappingKit |
| 字符串 | StrKit、StrPool |
| 集合/数组 | CollKit、ArrayKit |
| ID | IdKit |
| 函数和类型转换 | FunctionKit |
| 日期时间 | DateKit/相关 formatter |
| 反射 | ReflectKit/明确的元数据工具 |

## JSON 边界

- 3.0.x JsonKit 使用 tools.jackson databind。
- DEFAULT_OBJECT_MAPPER 用于普通 JSON。
- REDIS_OBJECT_MAPPER 启用 DefaultTyping，只处理受信任缓存数据。
- EventStore 使用 EventPayloadSerializer 和显式事件类型，不使用 Redis mapper。
- com.fasterxml.jackson.annotation 作为 Jackson 2/3 兼容注解包存在。

## 能力边界

### ✅ 擅长

- 工具选择、null/异常语义。
- JsonKit 与 Jackson 2/3 边界。
- Bean/集合/字符串/ID 常用操作。
- 避免重复工具封装。

### ⚠️ 需要素材

- 当前维护线。
- 输入类型和期望异常策略。
- JSON 使用场景：HTTP、缓存或事件。

### ❌ 超范围

- 把工具类当领域服务。
- 对不可信 JSON 启用 unrestricted polymorphism。
- 用 Kit 隐藏事务、网络或资源生命周期。

## 工作流

1. 搜索当前 Kit 中是否已有对应方法。
2. 读取签名、实现和测试，而非按名字猜语义。
3. 区分纯函数、全局 mapper 和有副作用工具。
4. 选最窄 API，保留 Optional/异常/泛型信息。
5. 对边界值和错误路径执行测试。

## 常见错误

- 继续使用已合并的 JacksonKit 名称。
- 用 Redis mapper 反序列化外部 payload。
- BeanKit 静默复制代替显式 Domain/PO 映射。
- StrKit/CollKit 判空后仍重复手写逻辑。
- 依赖高线 API 却未验证旧线。
- 捕获工具异常后返回伪成功。

## 输出与异常

说明工具全限定名、维护线、输入/输出、null 与异常语义。缺失时写“缺少：目标类型或维护线；补充方式：提供调用点与 POM”。

## 深度参考

- [JSON 与 Jackson](references/json-and-jackson.md)
- [Bean、字符串与集合](references/bean-string-collection.md)
- [ID、函数与反射](references/id-function-reflection.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

JSON、日志和异常不得暴露 Token、密码、隐私字段或私服凭据。

