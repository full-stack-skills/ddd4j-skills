# 源码证据索引

- `ddd4j-data-mybatis/.../mapper/Ddd4jMapper.java`：原生 MyBatis 最小 CRUD。
- `ddd4j-data-mybatis/.../repository/MybatisAggregateRepository.java`：无 Plus 轨道及生产查询警告。
- `ddd4j-data-mybatisplus/.../repository/MybatisAggregateRepository.java`：BaseMapper/Wrapper 轨道。
- `ddd4j-core/.../ddd/repository/Repository.java`：共同 SPI。
- `ddd4j-core/.../cqrs/query/{Query,PersistenceQueryScope}.java`：领域查询。
- `ddd4j-data-mybatisplus/.../inner/DataPermissionInnerInterceptor.java`：数据权限 SQL 注入。
- `Ddd4jAggregateFillInnerInterceptor.java`、`Ddd4jTenantContext.java`、SQL observation tests：填充、租户、观测。

同包同类名存在于两个 artifact，必须用 Maven 坐标确认实际轨道。
