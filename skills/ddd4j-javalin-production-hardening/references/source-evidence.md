# 源码证据路由

使用本技能时必须在目标 `ddd4j-javalin` 检出中重新确认：

- 当前分支、POM 模型、Maven Wrapper、JDK 与 Javalin 版本。
- `Ddd4jJavalinApplication`、配置对象、Web 生命周期、readiness、idempotency 和 CORS 实现。
- `Ddd4jJavalinRuntime`、`JavalinLifecycleParticipant` 是否已存在及其测试状态。
- JPA EntityManagerFactory、MQ、Outbox、调度器与 shutdown hook 的实际所有者。
- `docs/superpowers/specs/`、`plans/`、`reports/` 中当前事实源。
- GitHub Actions 最终 SHA 的必需 job，以及私有 Maven 远端元数据和空缓存消费者。

历史矩阵只能作为定位假设，不能替代当前源码、POM、测试、CI 和远端制品证据。

