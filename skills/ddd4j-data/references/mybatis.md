# MyBatis 与 MyBatis-Plus

原生轨道：Ddd4jMapper<P> + MybatisAggregateRepository，删除和生产查询 SQL 需显式实现。

Plus 轨道：BaseMapper<P> + 同名仓储，Query<M> 翻译为 Wrapper。

共同规则：M/P/Q/ID 五泛型、DomainObjectMapper、RepositoryRegistry、租户/数据范围/SQL observation。两个 artifact 含同包同类名，不要同时依赖。

