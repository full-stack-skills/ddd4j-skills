# 深度 FAQ

1. **Metrics 和 tracing 相同吗？** 不同。
2. **Noop 是错误吗？** 是允许降级但无观测。
3. **tenantId 能做 label 吗？** 通常高基数且敏感。
4. **Projection lag 怎么算？** 需要权威 head 与 position。
5. **指标名能改吗？** 属于监控契约变更。
6. **测试要启动 collector 吗？** 单元测 API，集成测 exporter。
7. **日志能替代 metrics 吗？** 不能。
8. **readiness 能从错误率推导吗？** 不应直接替代。
9. **MQ retry 如何计数？** 按 attempt/result 稳定标签。
10. **完成证据是什么？** 单元行为、导出链和告警演练。

