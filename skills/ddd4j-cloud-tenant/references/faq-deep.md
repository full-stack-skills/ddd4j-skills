# 深度 FAQ

1. **先选什么？** Cloud→Boot→ddd4j 主组合。
2. **备选等于主组合吗？** 不等于。
3. **配置存在等于服务可用吗？** 不等于。
4. **Context 只在线程内吗？** 还需异步/Reactor/Feign。
5. **旧 cmpt 能继续用吗？** 按当前硬切规范处理。
6. **Binder 名称能跨 Broker 通用吗？** 物理 destination 有差异。
7. **上游缺件怎么报？** BLOCKED(upstream)。
8. **CI 未启动怎么办？** BLOCKED(infrastructure)。
9. **能打印 Nacos 配置吗？** 敏感值必须脱敏。
10. **完成证据是什么？** 当前线源码、外部行为和远端消费层级。

