# Sa-Token

入口：StpKit、SaTokenSubject、SaTokenSubjectProvider、SaTokenSecurityConfigurer、SaTempKit、ApiKeyKit。

- 使用 StpKit.DEFAULT/ADMIN/USER 保持账号体系一致。
- 扩展字段通过 AuthConstants 和类型安全 getter。
- SaTempToken 使用短 TTL、单用途和删除/校验。
- SaMixCheckLogin/SaInternalCheck 需要 handler 行为测试。
- 请求结束验证 Subject 和 Sa-Token 上下文清理。

