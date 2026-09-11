---
name: ddd4j-mybatis
description: Use when implementing current ddd4j native MyBatis or MyBatis-Plus aggregate repositories, domain-to-PO mapping, Query translation, tenant/data-scope enforcement, aggregate fill, or SQL observation; not for legacy PaginationEntity/BaseService conventions.
license: Apache-2.0
---

# ddd4j MyBatis

## Overview

将 ddd4j 的 `AggregateRoot/Query/Repository` 契约适配到原生 MyBatis 或 MyBatis-Plus。领域模型与持久化对象必须分离，不能把 Wrapper 或 PO 泄漏到 Domain。

## 快速开始

- “实现 MybatisAggregateRepository。”
- “让 Query<M> 翻译为 MyBatis-Plus LambdaQueryWrapper。”
- “接入租户、数据权限和聚合填充。”
- “选择原生 MyBatis 还是 MyBatis-Plus 轨道。”

## 受众、路由与定制

- 仓储开发者：指定原生或 Plus 轨道和 M/P/Q/ID。
- 数据平台开发者：指定租户、数据权限、审计和观测要求。
- 审查者：指定只读检查、数据库方言及事务/并发风险。
- 普通 MyBatis 项目：转用 MyBatis 技能，不套用 ddd4j Repository。

输入不足时先列出两轨差异与暂定选择，再输出“缺少：artifact/M/P/Q/ID；补充方式：提供 POM 和类型定义”。

## 能力边界

### ✅ 擅长

1. 原生 `Ddd4jMapper<P>` + 五泛型 `MybatisAggregateRepository`。
2. MyBatis-Plus `BaseMapper<P>` + 同名仓储适配器。
3. `DomainObjectMapper<M,P>`、`DomainModelHelper` 和 `RepositoryRegistry`。
4. `Ddd4jTenantContext`、`DataScopeProvider`、数据权限、聚合填充、SQL observation。

### ⚠️ 需要素材

1. 选择原生 MyBatis 或 MyBatis-Plus。
2. 聚合根 M、PO P、Query Q、ID 和 Mapper 类型。
3. 表结构、事务、租户与删除语义。

### ❌ 超范围

1. 旧 `PaginationEntity`、`BaseServiceImpl`、固定 `@Param("model")` 规则。
2. 让领域实体继承 MyBatis-Plus `Model<T>`。
3. 猜测删除 SQL、表名或主键。

## 两条轨道

| 维度 | 原生 MyBatis | MyBatis-Plus |
|---|---|---|
| Mapper | `Ddd4jMapper<P>`，SQL 由 XML/注解显式提供 | `BaseMapper<P>` |
| 仓储 | 不依赖 MyBatis-Plus | 继承 `AbstractRepository<MP,P>` |
| 条件查询 | 默认内存过滤仅作兜底，生产应覆盖为 SQL | Query 翻译为 Wrapper |
| 删除 | 默认拒绝，业务仓储显式实现 | 可使用 BaseMapper 能力 |
| 映射 | `DomainObjectMapper<M,P>` | 同左 |

## 示例

```java
public final class OrderRepository
        extends MybatisAggregateRepository<OrderMapper, Order, OrderPO, OrderQuery, OrderId> {

    public OrderRepository(OrderMapper mapper) {
        super(mapper);
    }

    @Override
    public Order toModel(OrderPO po) {
        return new Order(new OrderId(po.getId()), po.getStatus());
    }

    @Override
    public OrderPO toPersistenceObject(Order model) {
        return new OrderPO(model.id().value(), model.status());
    }
}
```

导入哪个 `MybatisAggregateRepository` 必须由模块坐标决定；原生与 Plus 包名相同，不能凭 IDE 自动导入判断。

## 工作流

1. 确认目标模块和依赖轨道。
2. 定义领域聚合、PO 和 Query 的显式映射。
3. 让仓储注册到 `RepositoryRegistry`。
4. 接入租户、数据范围、审计填充和 SQL observation。
5. 用真实数据库验证 CRUD、Query 翻译、租户隔离、事务与并发。
6. 原生轨道的生产条件查询必须覆盖默认内存过滤。

## 常见错误

- 聚合根直接加 `@TableName`。
- 把 `Query<M>` 错绑成 PO 类型。
- 原生轨道未实现删除却假设默认可用。
- 生产继续使用原生仓储的内存过滤兜底。
- 用字符串拼接不可信数据范围 SQL。
- 忽略两个模块中同包同类名造成的依赖冲突。

## 输出与异常

必须注明所选轨道、五个泛型、映射、事务及隔离证据。缺少时输出“缺少：MyBatis 轨道或 M/P/Q/ID；补充方式：提供模块 POM 与领域/PO 类型”。

## 隐私与安全

测试使用隔离数据库和脱敏数据；SQL observation 不记录密码、Token 或敏感字段值。

## FAQ

1. **领域对象能继承 Model 吗？** 不能，当前边界是 AggregateRoot 与 PO 分离。
2. **为什么五个泛型？** 分别绑定 Mapper、聚合、PO、Query 和 ID。
3. **原生 MyBatis 默认支持删除吗？** 不支持，需显式 SQL。
4. **Query 为什么绑定聚合？** 保持领域层不依赖 PO。
5. **可以只跑 H2 吗？** 不足以证明目标数据库方言、事务与隔离。
6. **何时用 MyBatis-Plus？** 需要 Wrapper/BaseMapper 能力且能接受该依赖时。

## 深度参考

- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)
