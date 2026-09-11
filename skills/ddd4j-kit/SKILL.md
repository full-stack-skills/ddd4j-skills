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

## 快速开始

- “使用 `$ddd4j-kit` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-kit` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-kit` 给出实现选择、证据状态和剩余风险。”

## 受众与定制

- 开发者：提供目标维护线、POM、功能和验收行为。
- 架构师：指定只读边界审查、兼容性或迁移目标。
- 测试/发布人员：指定所需证据层级，不自动扩大到发布或生产操作。

可定制目标框架、允许实现、排除模块、兼容性要求和输出证据层级。输入不足时先给暂定判断，再列出“缺少：具体项；补充方式：所需路径或配置”。

## 常见问题

1. **是否按 Maven artifact 创建技能？** 不，按用户面对的功能域组织。
2. **是否能直接套用其他维护线？** 不能，先核对版本和源码。
3. **源码中有类就表示能力可用吗？** 不表示，还需注册和行为证据。
4. **测试未运行如何报告？** 标记 NOT RUN 或 BLOCKED。
5. **可以自动提交或发布吗？** 只有用户明确授权后才执行。
6. **找不到实现怎么办？** 说明缺失的模块或证据，不编造 API。
