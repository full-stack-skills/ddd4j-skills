# 深度 FAQ

1. **core 能依赖 Jackson 吗？** 以 CoreIndependenceTest 和 POM白名单为准。
2. **annotation 是运行时吗？** 注解 retention/消费者决定，不能统一假定。
3. **Repository 属于 data 吗？** 端口在 core，实现位于 data。
4. **CommandBus 属于 runtime 吗？** 接口在 core，装配在 runtime。
5. **Web 能直接改 Domain Context 吗？** 通过受控作用域绑定并释放。
6. **BOM 引入等于 Bean 可用吗？** 不等于。
7. **聚合模块能放代码吗？** 以当前 POM和源码为准，通常是聚合边界。
8. **如何验证架构？** CodeGraph、ArchUnit/规则测试、编译和运行分层验证。
9. **可以同时用 Spring 和 Guice 吗？** 需明确注册所有权，避免重复 SPI。
10. **跨线结构相同等于行为相同吗？** 不等于，需要行为和运行证据。
