# 深度 FAQ

1. **StpKit.USER 会自动携带扩展吗？** 取决于登录参数与模式。
2. **getExtraAs 如何转换？** 可传 Function 或 Class，当前内部使用 JsonKit。
3. **JWT 与 Redis 会话扩展一致吗？** 不应假定，按模式测试。
4. **SaTempToken 包含什么？** 登录、第三方身份、设备/来源等临时认证数据。
5. **checkTempToken 检查什么？** 非空、超时、解析和 loginId。
6. **永久临时 Token 合理吗？** 安全场景通常不合理，-1 必须有明确授权。
7. **ApiKey 与 Same-Token 一样吗？** 不是，边界和用途不同。
8. **SubjectProvider 做什么？** 将 Sa-Token 当前会话映射为 ddd4j Subject。
9. **内部调用能跳过用户权限吗？** 不能，内部身份与用户授权分别验证。
10. **如何安全排障？** 记录模式、账号体系、过期时间和脱敏指纹。
