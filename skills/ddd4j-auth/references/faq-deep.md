# 深度 FAQ

1. **三框架必须都启用吗？** 不，按项目选主实现。
2. **Subject 等于框架 Subject 吗？** 不等于，是统一抽象。
3. **Sa-Token extra 如何读取？** 使用 AuthConstants/StpKit 封装。
4. **Shiro Realm 属于 core 吗？** 不属于。
5. **SecurityContext 能进领域层吗？** 不应。
6. **OIDC 自动注册 SubjectProvider 吗？** 不自动。
7. **Same-Token 是用户认证吗？** 不是。
8. **临时 Token 能永久吗？** 安全默认不应。
9. **异步如何传播身份？** 使用运行时提供的受控 Context 传播并恢复。
10. **完成证据是什么？** Provider、异常、生命周期和真实请求测试。
