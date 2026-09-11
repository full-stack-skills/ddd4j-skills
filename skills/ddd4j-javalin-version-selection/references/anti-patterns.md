# 反模式

1. **跨线复制**：按 Javalin/JDK/Maven 适配。
2. **smoke 假绿**：要求真实 HTTP/Auth/DB/MQ 行为。
3. **Context 泄漏**：所有终态清理。
4. **固定 READY**：聚合真实依赖。
5. **证据混淆**：源码、测试、CI、发布分开。

