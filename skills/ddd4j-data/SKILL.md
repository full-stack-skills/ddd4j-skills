---
name: ddd4j-data
description: Use when choosing, implementing, or reviewing ddd4j persistence with JDBC, JDBI, JPA, MyBatis, MyBatis-Plus, R2DBC, Panache, EventStore, Projection, Outbox, transactions, tenants, or Domain-to-PO mapping.
license: Apache-2.0
---

# ddd4j Data

## Overview

先选择持久化模型，再选择技术：快照 Repository、Event Sourcing、Projection 和 Outbox 是不同职责，可组合但不能混淆事务边界。

## 技术选择

| 能力 | 实现 |
|---|---|
| 同步 SQL | JDBC、JDBI |
| ORM | JPA |
| Mapper | MyBatis、MyBatis-Plus |
| Reactive | R2DBC |
| Quarkus ORM | Panache |
| 事件存储 | JDBI/JPA/R2DBC/Panache/ESDB EventStore |
| 读模型 | Projection + 多运行时 scheduler/repository |
| 可靠发布 | transactional Outbox |

## 核心规则

1. Domain AggregateRoot 与 PO/Entity 分离。
2. Repository 端口在 core，实现位于 data。
3. Query 绑定领域模型；PO 字段通过 persistence scope/元数据映射。
4. EventStore append 要校验 expected version 和批次原子性。
5. Projection position 更新与读模型写入需明确事务/幂等。
6. Outbox 必须与业务写共享事务，再独立 claim/send/confirm。
7. 真实数据库测试证明方言、事务、并发和可见性。

## 能力边界

### ✅ 擅长

- 技术选型和 Domain/PO 映射。
- Repository、EventStore、Projection、Outbox。
- 租户、数据范围、加密字段。
- 同步/响应式事务边界。

### ⚠️ 需要素材

- 数据库、运行时和维护线。
- 聚合/PO/Query/ID。
- 一致性和并发要求。

### ❌ 超范围

- 把 H2 单测当生产数据库证明。
- 默认内存过滤用于生产大数据。
- 用 focused test 宣称事务/并发已验证。

## 工作流

1. 选择快照或事件溯源。
2. 定义 Aggregate/PO/Query 映射。
3. 选择 JDBC/JDBI/JPA/MyBatis/R2DBC/Panache。
4. 定义事务、租户、加密和审计。
5. 如需读模型/发布，加入 Projection/Outbox。
6. 执行真实数据库、回滚、并发和恢复测试。

## 常见错误

- AggregateRoot 直接成为框架 PO。
- 原生 MyBatis 内存过滤上生产。
- EventStore 与业务写各自提交。
- MAX(position)+1 在并发下分配全局位置。
- Projection 先推进 cursor 后写读模型。
- Outbox 发送成功但未确认/重复发送无幂等。

## 深度参考

- [存储选择](references/storage-selection.md)
- [MyBatis](references/mybatis.md)
- [EventStore](references/event-store.md)
- [Projection](references/projection.md)
- [Outbox 与事务](references/outbox-and-transactions.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

测试数据脱敏；SQL、事件和 Outbox 日志不得暴露凭据或隐私载荷。

