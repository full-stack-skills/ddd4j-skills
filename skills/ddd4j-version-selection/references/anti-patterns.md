# 反模式

1. **最新版偏见**：不收集 JDK/运行时就推荐 3.0.x；先固定约束。
2. **分支名推断**：把 quarkus 4.0.x 当 Quarkus 4；读取 quarkus-bom.version。
3. **工具链抹平**：全部改 Maven 4；保留旧线 Maven 3/POM 4.0。
4. **组合缺项**：只给 ddd4j，不给 Boot/Cloud/Javalin/Quarkus 和框架版本。
5. **发布假绿**：本地 build 或上传开始被称为可消费；要求远端空缓存验证。
6. **过时矩阵**：复制历史表不标日期/SHA；每次重读源码。

