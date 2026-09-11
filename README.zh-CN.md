<div align="center">

# ddd4j-skills

**面向当前 ddd4j 源码、维护线与生产交付流程的 Agent Skills**

[English](./README.md) | 简体中文

</div>

## 简介

本包将 ddd4j 专有契约与通用 Java、通用 DDD 方法论分离。技能必须以目标维护线的真实源码、POM、测试和运行证据为准，不把历史业务框架约定当作当前公共 API。

## 安装

```bash
npx skills add full-stack-skills/ddd4j-skills
```

按需安装：

```bash
npx skills add full-stack-skills/ddd4j-skills --skill <skill-name>
```

## 技能列表（10）

| 技能 | 适用场景 |
|---|---|
| `ddd4j-version-selection` | 选择兼容的 ddd4j、Boot、Cloud、Javalin、Quarkus、JDK、Maven 和 POM 版本 |
| `ddd4j-architecture` | 设计和审查 ddd4j 模块边界、DDD/CQRS 分层、端口、适配器和运行时 |
| `ddd4j-annotation` | 选择和审查 ddd4j 的 DDD、CQRS、API、ORM 注解及其消费者 |
| `ddd4j-bom` | 治理 ddd4j parent、dependencies、BOM 导入、Maven 模型和版本所有权 |
| `ddd4j-core` | AggregateRoot、CQRS、DomainEvent、Repository、Context、Subject、Cache 等核心契约 |
| `ddd4j-kit` | 选择 ddd4j JSON、Bean、字符串、集合、标识、函数和反射工具 |
| `ddd4j-mybatis` | 原生 MyBatis/MyBatis-Plus 聚合仓储、Domain/PO 映射、租户与数据权限 |
| `ddd4j-validation` | ddd4j-web-validation 四个公开约束及维护线兼容 |
| `ddd4j-satoken` | StpKit、Subject Bridge、认证模式、临时 Token 和 API Key |
| `ddd4j-javalin-production-hardening` | ddd4j-javalin 多分支生产加固、TDD、CI 与私有 Maven 发布 |

## 边界

- 普通 Java 库/API：使用 `java-skills`。
- 通用 DDD 建模和架构方法：使用 `ddd-skills`。
- ddd4j 源码契约、适配器、维护线和发布门禁：使用本包。

## 许可证

Apache-2.0，详见 [LICENSE](LICENSE)。
