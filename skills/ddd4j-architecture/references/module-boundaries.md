# 模块边界

- ddd4j-annotation：元数据，不承担运行时实现。
- ddd4j-core：DDD/CQRS/Auth/Cache/Context/Health 等框架无关契约。
- ddd4j-auth/data/mq/web/cache/metrics：能力实现与适配器集合。
- ddd4j-runtime：Spring、Guice、Quarkus 运行时绑定。
- ddd4j-extensions：Akka、Excel、Jackson/PF4J/QLExpress 等可选能力。
- ddd4j-ddd-rules：Clean/COLA 等架构检查。
- ddd4j-parent/dependencies/bom：构建和消费治理。

使用时以当前根 POM和 CodeGraph 为准。

