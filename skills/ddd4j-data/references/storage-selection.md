# 存储选择

- JDBC：最少抽象、显式 SQL。
- JDBI：SQL Object/handle 和轻量事务。
- JPA：实体生命周期和 ORM。
- MyBatis：显式 Mapper/XML。
- MyBatis-Plus：BaseMapper/Wrapper 与 ddd4j Query 翻译。
- R2DBC：响应式数据库链路。
- Panache：Quarkus 持久化适配。

选择依据：运行时、事务、查询复杂度、响应式需求、方言和团队能力。
