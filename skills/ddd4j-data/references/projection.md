# Projection

核心：ProjectionRunner、ProjectionPositionRepository、ProjectionService、ProjectionMetrics。

适配：Spring、Javalin、Quarkus、Micronaut、Vert.x、Helidon、Dropwizard；位置存储可用 JDBI/JPA/R2DBC/Panache。读模型写入和 position 推进需幂等且明确事务边界。

