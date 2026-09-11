# 深度 FAQ

1. **接口和实现放哪？** 端口 core，绑定 runtime。
2. **能同时注册两个 CommandBus 吗？** 需明确路由，默认避免冲突。
3. **SubjectProvider 谁注册？** 目标 runtime。
4. **Guice 等于 Spring 吗？** 不等于。
5. **Quarkus 何时注册？** 以 CDI observer/producer 当前实现为准。
6. **ready 等于 started 吗？** 不等于。
7. **如何回滚？** 记录完成项并逆序关闭。
8. **close 能抛异常吗？** 需聚合并继续关闭其他资源。
9. **异步 Context 怎么办？** 使用运行时传播机制并恢复。
10. **完成证据是什么？** runtime-testkit 和真实框架启动/关闭测试。
