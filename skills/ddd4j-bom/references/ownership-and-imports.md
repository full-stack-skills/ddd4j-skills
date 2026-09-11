# 职责与导入

- ddd4j-parent：插件管理、构建、测试、发布约定。
- ddd4j-dependencies：第三方库版本和必要替代坐标。
- ddd4j-bom：面向消费者的 ddd4j artifact 版本集合。
- adapter dependencies/BOM：只拥有 Boot、Cloud、Javalin、Quarkus 专属依赖。

审查顺序：直接声明→父级→导入 BOM 顺序→effective POM→dependency tree。

