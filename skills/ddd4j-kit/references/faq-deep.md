# 深度 FAQ

1. **JacksonKit 还存在吗？** 当前能力已合并到 JsonKit。
2. **默认 mapper 和 Redis mapper 相同吗？** 不同。
3. **Redis mapper 能处理外部 JSON 吗？** 不应。
4. **事件为何不用 DefaultTyping？** 避免任意类多态攻击。
5. **BeanKit 能替代 DomainObjectMapper 吗？** 不能保证领域语义。
6. **StrKit 与 Spring StringUtils 如何选？** ddd4j 内部优先当前 Kit 契约，适配层按框架边界。
7. **工具返回 null 怎么办？** 读取具体签名和测试，不统一猜测。
8. **Kit 能访问数据库吗？** 不应承载该资源生命周期。
9. **旧线工具都一致吗？** 不保证。
10. **何时新增工具？** 多模块复用、语义稳定且有边界测试时。

