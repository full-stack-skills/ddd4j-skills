---
name: ddd4j-annotation
description: Use when selecting, applying, reviewing, or extending current ddd4j annotations for DDD metadata, CQRS events, API behavior, ORM mapping, idempotency, auditing, or tenant fields.
license: Apache-2.0
---

# ddd4j Annotation

## Overview

按注解的消费者和运行时语义选择注解，不能仅凭名称推断它会注册 Bean、持久化字段或触发事件。

## 快速路由

| 需求 | 家族 |
|---|---|
| 领域分类和元数据 | ddd、Contract、BusinessType |
| Create/Update/Delete 事件 | cqrs |
| 幂等、模块、操作日志、原始响应 | api |
| Domain/PO 映射、租户、审计、排序 | orm |

## 使用规则

1. 先查看 Retention、Target、默认值和消费者。
2. RUNTIME 只表示可反射，不等于框架自动处理。
3. ORM 注解由 DomainModelHelper、Repository 或拦截器消费。
4. API 注解需由 Web/Runtime 适配器实现行为。
5. 新增注解同时增加独立性、默认值、Target 和消费者测试。
6. 跨维护线核对包名和 Java/Jakarta 差异。

## 能力边界

### ✅ 擅长

- Contract/BusinessType/DDDAnnotation。
- ApiIdempotent、ApiModule、ApiOperationLog、RawResponse。
- CreateEvent、UpdateEvent、DeleteEvent。
- DomainField、TenantId、SystemId、BizKey、OnCreate/OnUpdate、OrderBy。

### ⚠️ 需要素材

- 当前维护线。
- 注解目标元素和预期消费者。
- Web、Data 或 Runtime 适配器。

### ❌ 超范围

- 仅加注解就宣称功能生效。
- 把 Spring/Quarkus 注解当 ddd4j 注解。
- 不经兼容审查改变 retention/target。

## 示例

~~~java
public final class OrderPO {
    @BizKey
    private String orderNo;

    @TenantId
    private String tenantId;

    @OnCreate
    private Instant createdAt;

    @OnUpdate
    private Instant updatedAt;
}
~~~

示例只表达元数据；是否填充和隔离取决于 Data 适配器。

## 常见错误

- 把 DDDAnnotation 当 Component。
- 使用 ApiIdempotent 却未装配 IdempotencyGuard。
- DomainField 映射后仍让 Domain 引用 PO。
- TenantId 字段存在但请求上下文未绑定租户。
- OnCreate/OnUpdate 没有拦截器或仓储支持。
- CQRS 事件注解没有对应发布测试。

## 输出与异常

输出“注解全限定名、Retention、Target、属性、消费者、验证测试”。缺少消费者时写“缺少：运行时处理器；补充方式：确认目标 Web/Data/Runtime 模块”。

## 深度参考

- [DDD 与契约](references/ddd-and-contract.md)
- [API 与 CQRS](references/api-and-cqrs.md)
- [ORM](references/orm.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

日志、租户和认证相关注解不得导致敏感字段或完整请求体泄露。

