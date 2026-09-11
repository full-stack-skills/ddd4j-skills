---
name: ddd4j-core
description: Use when implementing or reviewing current ddd4j domain models, aggregate roots, CQRS commands/queries, domain events, repository SPI, context, subject, cache, or health contracts; not for legacy io.hiwepy.boot CRUD conventions.
license: Apache-2.0
---

# ddd4j Core

## Overview

基于当前 `io.ddd4j.core` 公共契约指导领域建模和框架无关代码。核心边界是：`ddd4j-core` 定义 DDD/CQRS/SPI，Spring、Guice、Quarkus、Javalin、MyBatis 等只在适配层装配。

## 快速开始

- “用 ddd4j 建一个事件溯源聚合。”
- “实现 Command、CommandExecutor 和 CommandBus 调用。”
- “审查领域层是否错误依赖 Spring/MyBatis。”
- “解释 ThreadContext、Contexts 和 Subject 的边界。”

## 受众、路由与定制

- 领域开发者：传入聚合策略、目标维护线和业务不变量。
- 适配器开发者：传入运行时、仓储/总线实现和事务边界。
- 审查者：要求只读检查并指定关注 DDD、CQRS、上下文或 SPI。
- 非 ddd4j 项目：转用通用 DDD/Java 技能，不套用本技能类型。

输入不足时先基于当前检出给出“暂定结论”，再列出“缺少：具体项；补充方式：路径/分支/契约”。

开始前确认当前分支；1.0.x、2.0.x、3.0.x API 不能凭名称假定一致。

## 能力边界

### ✅ 擅长

1. `AggregateRoot<ID>` 的 Active Record 与 Event Sourcing 两种模式。
2. `Command`、`CommandExecutor`、`CommandBus`、`Result<R>` 写侧契约。
3. `Query<M>`、`PersistenceQueryScope<M,P>` 与 `Repository<M,ID>`。
4. `DomainEvent<ID>` 元数据、发布、回放和事件处理器。
5. `Contexts`/`ThreadContext`、`Subject`、`Cache` 等框架无关 SPI。

### ⚠️ 需要素材

1. 指定维护线及其源码/POM。
2. 领域模型、持久化策略和事务边界。
3. 运行时适配器及真实验收行为。

### ❌ 超范围

1. `io.hiwepy.boot.api.*` 的 BaseEntity、PaginationEntity、ApiRestResponse。
2. 把 Spring 注解语义当成所有运行时的核心契约。
3. 替代具体 MyBatis/JPA/Jackson/Sa-Token 适配技能。

## 核心规则

| 主题 | 当前契约 |
|---|---|
| 聚合根 | 继承 `AggregateRoot<ID>`，标识实现 `Serializable` |
| 持久化模式 | Active Record 与 Event Sourcing 二选一，同一聚合不得混用 |
| 事件 | 子类保留无参构造；用 `registerEvent`，回放用 `loadFromHistory` |
| 命令 | `Command` 表达意图；由 `CommandExecutor` 执行，经 `CommandBus.execute` 调度 |
| 查询 | `Query<M>` 绑定领域模型；需要 PO 字段时显式 `persistence(P.class)` |
| 仓储 | 领域只依赖 `Repository`；实现由 data/runtime 适配层注册 |
| 上下文 | 请求/线程结束必须释放作用域，不能让 Subject 或租户信息泄漏 |
| 缓存 | 只依赖 `Cache` SPI；跨实例原子语义必须由实现证明 |

## 示例

```java
public final class Order extends AggregateRoot<OrderId> {
    private OrderStatus status;

    public void pay() {
        if (status == OrderStatus.PAID) {
            throw new IllegalStateException("订单已支付");
        }
        registerEvent(new OrderPaid(id()));
    }

    @EventHandler
    void apply(OrderPaid event) {
        status = OrderStatus.PAID;
    }
}
```

若使用事件溯源，就持久化 `pullDomainEvents()`，不要再调用快照式 `save()/update()`。

## 工作流

1. 从当前源码和测试确认维护线契约。
2. 判断聚合采用快照还是事件溯源。
3. 让 Domain 只依赖 core API/SPI。
4. 在 data/runtime 模块实现仓储、总线和发布器。
5. 用聚合不变量、事件回放、命令结果和上下文清理测试验证。

## 常见错误

- 延续旧 `BaseEntity/Model<T>` 继承链。
- 在核心领域层直接依赖 Spring/MyBatis Wrapper。
- 同时保存聚合快照和未提交事件。
- 将 `DomainEvent.source()` 当成完整 `EntityIdPath`。
- 忽略 `Repository` 默认方法可能抛 `UnsupportedOperationException`。
- 只绑定 `ThreadContext` 而不在 finally/作用域关闭时清理。

## 输出与异常

引用具体包名、源码路径和维护线。找不到符号时输出“缺少：当前分支中的符号或模块；补充方式：确认分支、POM 与源码路径”，不得用旧项目类型代替。

## 能力路由

- 模块边界和依赖方向：交给 **`ddd4j-architecture`**。Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-architecture`。
- 注解语义和消费者：交给 **`ddd4j-annotation`**。Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-annotation`。
- Maven/BOM/版本所有权：交给 **`ddd4j-bom`**。Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-bom`。
- JSON、Bean、字符串、集合与 ID 工具：交给 **`ddd4j-kit`**。Install: `npx skills add full-stack-skills/ddd4j-skills --skill ddd4j-kit`。

## 隐私与安全

示例使用虚构订单和标识；不要输出真实 Token、租户数据、用户资料或私服凭据。

## FAQ

1. **还能用 BaseEntity 吗？** 只有外部项目明确依赖它时；它不是当前 ddd4j-core 契约。
2. **AggregateRoot 必须事件溯源吗？** 不必，但同一聚合不要混用两种模式。
3. **Query 能引用 PO 吗？** 通过显式持久化作用域，领域 Query 本身绑定聚合根。
4. **Repository 是 MyBatis 专用吗？** 不是，它是 ORM 无关 SPI。
5. **DomainService 一定是 Spring Bean 吗？** 不能跨运行时这样假定。
6. **完成证明是什么？** 当前分支源码、相关测试与实际运行时适配验证。

## 深度参考

- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)
