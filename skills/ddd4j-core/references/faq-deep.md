# 深度 FAQ

1. **Active Record 是否意味着领域依赖 MyBatis？** 否，调用 RepositoryRegistry。
2. **EventHandler 如何解析？** 当前线优先注解，并保留命名约定兼容；以源码为准。
3. **事件为何要无参构造？** 支持 Jackson 回读和事件回放。
4. **source() 是否保留聚合路径？** 它是字符串兼容视图，完整语义看 EntityIdPath。
5. **ThreadContext 会深拷贝对象吗？** 当前只复制资源 Map，值保留引用。
6. **Query 的 current 从几开始？** 当前源码从 1 开始。
7. **size=-1 是什么？** 当前 Query 表示不分页；适配器必须保持语义。
8. **Core 能依赖 Lombok/Jackson 吗？** 以 CoreIndependenceTest 和当前 POM 的白名单为准。
9. **能把 3.0.x 结论用于 1.0.x 吗？** 不能，需逐线验证。
10. **何时需要 runtime 技能？** 当问题进入 DI、总线注册、生命周期或框架装配。
