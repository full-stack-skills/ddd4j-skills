# 反模式

1. **领域即 PO**：AggregateRoot 加表注解；使用 DomainObjectMapper 分离。
2. **误导入同名类**：依赖原生模块却引用 Plus 语义；先看 artifact。
3. **内存过滤上生产**：原生默认 findList 兜底被当 SQL；覆盖为 Mapper 动态 SQL。
4. **猜测删除**：原生 Ddd4jMapper 未定义 delete；显式实现。
5. **数据范围字符串失控**：拼入不可信 SQL；provider 必须输出受控表达式。
