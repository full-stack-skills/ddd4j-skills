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

## 技能列表（39）

| 技能 | 适用场景 |
|---|---|
| `ddd4j-version-selection` | 选择兼容的 ddd4j、Boot、Cloud、Javalin、Quarkus、JDK、Maven 和 POM 版本 |
| `ddd4j-boot-version-selection` | 按 Spring Boot、JDK、Maven 基线选择 13 条 ddd4j-boot 维护线 |
| `ddd4j-boot-architecture` | 设计 ddd4j-boot 模块边界和 Spring Boot 集成职责 |
| `ddd4j-boot-bom` | 管理 ddd4j-boot parent、dependencies、BOM、effective POM 和版本所有权 |
| `ddd4j-boot-autoconfiguration` | 开发条件自动配置、Properties、用户覆盖、imports 和生命周期 |
| `ddd4j-boot-auth` | 在 ddd4j-boot 中集成 Sa-Token、Shiro 和 Spring Security |
| `ddd4j-boot-data` | 集成 JDBC、JPA、MyBatis、迁移、事务、Projection 和 Outbox |
| `ddd4j-boot-cache` | 配置本地缓存、Redis、Redisson、JetCache、TTL、CAS 和幂等 |
| `ddd4j-boot-mq` | 配置多 Broker、Listener、ACK、重试、Readiness 和关闭 |
| `ddd4j-boot-web` | 构建 MVC/WebFlux Context、错误、认证、校验、幂等、CORS 和 Readiness |
| `ddd4j-boot-observability` | 配置 Actuator、健康、指标、追踪、日志、监控和 OpenTelemetry |
| `ddd4j-boot-extensions` | 集成 Akka、Excel、QLExpress、QR Code、Monitor 等扩展 |
| `ddd4j-boot-testing` | 测试自动配置、维护矩阵、HTTP、数据库、Redis 和 Broker |
| `ddd4j-boot-release` | 验证和发布 13 条维护线、CI 与空缓存消费 |
| `ddd4j-architecture` | 设计和审查 ddd4j 模块边界、DDD/CQRS 分层、端口、适配器和运行时 |
| `ddd4j-annotation` | 选择和审查 ddd4j 的 DDD、CQRS、API、ORM 注解及其消费者 |
| `ddd4j-bom` | 治理 ddd4j parent、dependencies、BOM 导入、Maven 模型和版本所有权 |
| `ddd4j-core` | AggregateRoot、CQRS、DomainEvent、Repository、Context、Subject、Cache 等核心契约 |
| `ddd4j-kit` | 选择 ddd4j JSON、Bean、字符串、集合、标识、函数和反射工具 |
| `ddd4j-data` | 选择 JDBC、JDBI、JPA、MyBatis、R2DBC、Panache、EventStore、Projection、Outbox 和事务 |
| `ddd4j-web` | 在多运行时应用统一 HTTP、Context、错误、校验、认证、幂等、CORS 和 Readiness 契约 |
| `ddd4j-auth` | 通过 ddd4j Subject 统一选择和集成 Sa-Token、Shiro、Spring Security |
| `ddd4j-cache` | 选择本地缓存、Redis、Redisson、JetCache、Memcached、TTL、锁和 CAS |
| `ddd4j-mq` | 选择和运行 Kafka、RabbitMQ、Pulsar、RocketMQ、MQTT、NATS、SQS、ACK 与生命周期 |
| `ddd4j-metrics` | 设计 Projection、Web、MQ、Cache、Runtime 和 OpenTelemetry 指标 |
| `ddd4j-runtime` | 集成 Spring、Guice、Quarkus CDI、Micronaut、Vert.x、Helidon 和 Dropwizard 运行时 |
| `ddd4j-extensions` | 选择 Excel、License、Monitor、OpenTelemetry、PF4J、QLExpress、QR Code 和 Validation 扩展 |
| `ddd4j-javalin-production-hardening` | ddd4j-javalin 多分支生产加固、TDD、CI 与私有 Maven 发布 |
| `ddd4j-javalin-version-selection` | 选择 6.7.x、7.1.x、7.2.x Javalin 维护线 |
| `ddd4j-javalin-architecture` | 设计 Javalin 模块与集成边界 |
| `ddd4j-javalin-runtime` | 管理启动、SPI、Readiness、Drain、回滚、Hook 和关闭 |
| `ddd4j-javalin-auth` | 集成 Sa-Token、Shiro、OIDC/Keycloak |
| `ddd4j-javalin-data` | 集成 MyBatis、JPA/PostgreSQL、Repository、事务、EventStore 和 Outbox |
| `ddd4j-javalin-web` | 构建路由、Context、错误、CORS、认证、校验、幂等和健康检查 |
| `ddd4j-javalin-mq` | 装配 MQ Listener、ACK、重试、Readiness 和关闭 |
| `ddd4j-javalin-cache` | 选择本地/分布式缓存、CAS、TTL 和幂等后端 |
| `ddd4j-javalin-extensions` | 组合 Guice Module、业务覆盖和扩展生命周期 |
| `ddd4j-javalin-testing` | 测试 HTTP、Keycloak、PostgreSQL、MQ、Docker、端口和生命周期 |
| `ddd4j-javalin-release` | 验证和发布三条维护线 |

## 边界

- 普通 Java 库/API：使用 `java-skills`。
- 通用 DDD 建模和架构方法：使用 `ddd-skills`。
- ddd4j 源码契约、适配器、维护线和发布门禁：使用本包。

## 许可证

Apache-2.0，详见 [LICENSE](LICENSE)。
