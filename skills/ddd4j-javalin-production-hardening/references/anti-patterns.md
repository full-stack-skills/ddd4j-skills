# 反模式

1. **范围漂移**：用户要求 Javalin，却转向 Quarkus/通用 ddd4j；保持目标仓库，只有实证依赖阻塞才升级。
2. **机械统一工具链**：把 7.1.x 改成 Maven 4；逐线保留 JDK/Maven/POM 契约。
3. **固定 READY**：readiness 不检查依赖；聚合 required/optional participant 状态。
4. **本地幂等冒充集群幂等**：生产多实例继续使用 Caffeine；要求共享 CAS 实现。
5. **活动冒充完成**：push、CI 启动或上传日志被当成功；等待终态并做空缓存消费。
