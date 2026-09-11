# 反模式

1. **硬编码扩展键**：散落 uuid/orgId；使用 AuthConstants 与 StpKit。
2. **账号体系混用**：DEFAULT 登录却用 USER 校验；入口到授权保持一致。
3. **临时 Token 当会话**：长 TTL、无用途约束；短时、可撤销、最小权限。
4. **Subject 泄漏**：请求结束不清理；验证生命周期测试。
5. **打印凭据**：日志输出完整 Token/API Key；仅记录脱敏指纹。
