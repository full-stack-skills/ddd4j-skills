# 反模式

1. **旧类名继续传播**：引用 JacksonKit；改为当前 JsonKit。
2. **代际导包错误**：3.0.x 使用旧 databind 包；核对 tools.jackson 与 annotations。
3. **不安全多态**：对外部 payload 开 unrestricted default typing；使用显式类型/白名单。
4. **一个 mapper 管所有场景**：HTTP、缓存、事件共享可变配置；分别构造并隔离。
5. **只看 POM 声明**：忽略 effective POM 和运行期缺类；执行依赖树与集成测试。
