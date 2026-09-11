# 反模式

1. **Context 泄漏**：只清理成功路径；覆盖异常/异步。
2. **固定 READY**：不查依赖；聚合 participant。
3. **宽松 CORS**：生产 anyHost；明确 allowlist。
4. **本地幂等冒充集群**：使用共享 CAS。
5. **适配器漂移**：只测一个运行时；用 testkit 对齐。

