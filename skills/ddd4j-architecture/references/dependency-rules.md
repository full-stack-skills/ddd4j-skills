# 依赖规则

1. 依赖箭头从适配器指向核心端口。
2. Domain 不依赖框架实体、Wrapper、HTTP Context。
3. Runtime 负责把 CommandBus、Publisher、SubjectProvider 等注册到 SPI。
4. Data 将 Domain 与 PO 显式映射。
5. Web 在请求边界绑定并释放 Context/Subject。
6. MQ/Cache 实现必须声明单机、集群和原子语义。
7. Parent/BOM 管理构建，不替代功能实现。
