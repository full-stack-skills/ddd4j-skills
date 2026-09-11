# 深度 FAQ

1. **Retention.RUNTIME 等于自动生效吗？** 不等于。
2. **Contract 做什么？** 标识可审计契约注解。
3. **DDDAnnotation 是 Spring Bean 吗？** 不能这样假定。
4. **ApiIdempotent 谁执行？** Web/Runtime 的幂等处理器。
5. **DomainField 谁读取？** 领域元数据和数据适配器。
6. **TenantId 自动隔离吗？** 需租户上下文和拦截器。
7. **OnCreate 会自动写时间吗？** 需仓储/拦截器实现。
8. **RawResponse 会绕过安全检查吗？** 只应影响响应包装。
9. **能修改注解默认值吗？** 属于公共契约变更，要跨线测试。
10. **新增注解最少测什么？** Retention、Target、默认值、独立性和消费者行为。
