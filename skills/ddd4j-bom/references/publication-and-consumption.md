# 发布与消费

1. clean 构建和完整测试。
2. 串行 deploy，记录模块总数和退出码。
3. 检查远端 metadata、timestamped SNAPSHOT 和 sidecar。
4. 新建隔离 Maven 本地仓库并使用 -U。
5. 消费 parent、dependencies、BOM 和代表性 JAR。
6. CI、Security 和生产验收分别报告。

RFC9457 JSON 404 或模块中途失败属于 PARTIAL，不是 PASS。
