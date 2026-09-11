---
name: ddd4j-validation
description: Use when applying or extending current ddd4j-web-validation constraints AllowableValues, PhoneNumber, NumberValue, or StringDateValue, including javax/jakarta maintenance-line compatibility and validator behavior.
license: Apache-2.0
---

# ddd4j Validation

## Overview

使用当前 `io.ddd4j.web.validation.constraints` 的四个约束。先确认维护线：3.0.x 使用 Jakarta Validation，旧线可能仍是 javax 代际。

## 快速开始

- “用 AllowableValues 限制状态值。”
- “用 PhoneNumber 校验国际号码。”
- “审查 StringDateValue 的空值与严格日期行为。”
- “把校验修改同步到三条维护线。”

## 受众、路由与定制

- API 开发者：指定字段、空值策略、消息和维护线。
- 校验器维护者：指定约束 API、边界样例与 javax/jakarta 目标。
- 审查者：指定只读检查和隐私要求。
- 通用 Bean Validation 问题：转用通用校验技能。

输入不足时先展示当前 3.0.x 精确 API，再输出“缺少：维护线/空值/格式契约；补充方式：提供分支和 DTO 字段”。

## 能力边界

### ✅ 擅长

1. `@AllowableValues(allows, nullable)`。
2. `@PhoneNumber(lang)`。
3. `@NumberValue(regex)`。
4. `@StringDateValue(pattern)` 与对应 Validator。

### ⚠️ 需要素材

1. 当前维护线和 validation API 代际。
2. 字段是否允许 null/空串。
3. 国际区号、日期格式或数字正则。

### ❌ 超范围

1. 名为 `AllowedValues` 且使用数组属性 `values` 的旧写法。
2. 用校验注解替代领域不变量。
3. 通用 Hibernate Validator 配置大全。

## 精确 API

```java
public final class CreateOrderRequest {
    @AllowableValues(allows = "CREATED,PAID,CANCELLED", nullable = false,
            message = "订单状态不合法")
    private String status;

    @PhoneNumber(lang = "CN", message = "手机号格式不正确")
    private String phone;

    @NumberValue(regex = "^[0-9]+$", message = "编号只能包含数字")
    private String number;

    @StringDateValue(pattern = "yyyy-MM-dd HH:mm:ss", message = "时间格式错误")
    private String occurredAt;
}
```

`allows` 是字符串，不是 `String[] values`。具体分隔和空值行为必须以当前 Validator 测试为准。

## 工作流

1. 打开当前分支的注解和 Validator 源码；注意 `NumberValue` 和 `PhoneNumber` 对 null 没有内置放行，应与 `@NotNull`/调用契约共同测试。
2. 明确 null、空串、默认 message 和格式行为。
3. 在 DTO/API 边界使用约束，领域聚合内部仍维护不变量。
4. 新增失败、成功、null/空串、边界格式测试。
5. 跨线移植时仅调整 javax/jakarta 和 Java 语法，不改变行为。

## 常见错误

- 写成 `AllowedValues` 或 `values={}`。
- 假设空串与 null 行为相同。
- 用 `@DateTimeFormat` 当成 Bean Validation。
- 只测一个合法值，不测非法、空值和边界。
- 把 CN 手机正则硬编码为唯一国际规则。
- 从 3.0.x 复制 Jakarta import 到旧线。

## 输出与异常

输出注解全限定名、属性、维护线和测试行为。缺少时输出“缺少：目标维护线或空值策略；补充方式：提供分支与字段契约”。

## 隐私与安全

手机号示例必须虚构或脱敏；不得在校验日志中输出完整号码和请求载荷。

## FAQ

1. **名称是 AllowedValues 吗？** 不是，当前公开注解是 AllowableValues。
2. **allows 是数组吗？** 不是，当前 API 是字符串。
3. **校验能替代领域规则吗？** 不能，只保护输入边界。
4. **PhoneNumber 只支持中国号码吗？** `lang` 指定区域，行为由 libphonenumber 验证。
5. **空串一定失败吗？** 不要假定，读取当前 Validator 并测试。
6. **跨线只改 import 就够吗？** 还要跑各线编译与行为测试。

## 深度参考

- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)
