# 深度 FAQ

1. **所有运行时 API 相同吗？** 不同，行为契约一致。
2. **Context 放 Domain 吗？** 领域通过抽象读取，不依赖框架。
3. **401 与 403 如何分？** 未认证与权限不足。
4. **Validation 属于领域规则吗？** 只保护输入边界。
5. **Caffeine 能生产幂等吗？** 多实例不能。
6. **readiness 能固定吗？** 不能。
7. **WebFlux Context 用 ThreadLocal 吗？** 需响应式传播适配。
8. **异步如何清理？** 完成/异常回调恢复。
9. **RawResponse 能绕过认证吗？** 只能影响包装。
10. **完成证据是什么？** 各 adapter 的真实 HTTP contract。

