---
name: ddd4j-version-selection
description: Use when choosing compatible ddd4j, ddd4j-boot, ddd4j-cloud, ddd4j-javalin, or ddd4j-quarkus versions for a new project, upgrade, migration, or maintained release line.
license: Apache-2.0
---

# ddd4j 版本选择

## Overview

选择的是完整兼容元组，不是单个“最新版本”。先固定 JDK、构建工具和运行时，再选择 ddd4j 及适配项目。

## 快速开始

- “JDK 17 的 Spring Boot 3.4 项目应该选哪条 ddd4j？”
- “Javalin 7.1 能否使用 ddd4j 3.0.x？”
- “Spring Cloud 2024.0.x 对应哪些 Boot 和 ddd4j 版本？”
- “Quarkus 4.0.x 为什么仍使用 Quarkus 3.38？”

## 输入契约

至少收集：

1. 项目是新建、升级还是维护。
2. JDK 与 Maven 可用版本。
3. Spring Boot/Cloud、Javalin 或 Quarkus 目标版本。
4. 是否必须使用 POM 4.0/Maven 3。
5. 是否要求远端 SNAPSHOT 可消费和 CI 已验证。

缺失时先给暂定候选，再输出“缺少：具体约束；补充方式：提供 POM、java -version、mvn -version”。

## 决策顺序

1. 用 JDK 锁定 ddd4j 主线：Java 8→1.0.x，Java 17→2.0.x，Java 21→3.0.x。
2. 用运行时锁定适配项目维护线。
3. 校验 Maven/POM Model：1.x/2.x 通常为 Maven 3/POM 4.0；3.x 为 Maven 4/POM 4.1。
4. 校验上游框架精确版本。
5. 查询私有 Maven 元数据和最终 SHA；未验证时标为 NOT VERIFIED。
6. 输出推荐、备选、不兼容、未验证四类。

## 快速矩阵

| ddd4j | JDK | Maven/POM | Boot |
|---|---:|---|---|
| 1.0.x | 8 | Maven 3 / 4.0.0 | Boot 2.3–2.7 |
| 2.0.x | 17 | Maven 3 / 4.0.0 | Boot 3.0–3.5 |
| 3.0.x | 21 | Maven 4 / 4.1.0 | Boot 4.0–4.1 |

完整 Boot、Cloud、Javalin、Quarkus 矩阵见 [兼容矩阵](references/compatibility-matrix.md)。

## 输出格式

| 字段 | 内容 |
|---|---|
| 推荐组合 | JDK、Maven、POM、ddd4j、适配项目、框架 |
| 选择理由 | 命中的源码矩阵和约束 |
| 不兼容项 | 冲突字段与原因 |
| 证据状态 | SOURCE / TEST / CI / PUBLISHED / CONSUMED |
| 后续验证 | 精确命令、分支和坐标 |

## 能力边界

### ✅ 擅长

- 五仓库版本组合选择。
- Maven 3/4 和 POM 4.0/4.1 边界。
- 主组合、兼容备选和升级路径。
- 识别本地成功与远端可消费的差别。

### ⚠️ 需要素材

- 当前 POM、分支或目标框架版本。
- 私服访问条件。
- 历史线是否允许升级 JDK/Maven。

### ❌ 超范围

- 猜测未发布版本可用。
- 自动升级依赖或切换分支。
- 用分支名代替 POM、CI 和远端证据。

## 常见错误

1. 给所有项目推荐最高 ddd4j 主线。
2. 把 Javalin 7.1.x 提升到 Maven 4。
3. 把 Quarkus adapter 版本当 Quarkus Platform 版本。
4. 只看 Cloud 分支名，不检查 Boot parent。
5. 把 deploy 上传开始当发布完成。
6. 把 Security SKIPPED 写成 PASS。

## 深度参考

- [兼容矩阵](references/compatibility-matrix.md)
- [证据与门禁](references/evidence-and-gates.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出 Maven settings、Token、密码或带签名的私服 URL；仅报告凭据来源和脱敏错误。

## 受众与定制

- 新项目开发者提供 JDK 和目标运行时。
- 维护者提供现有 POM、分支和升级限制。
- 发布人员指定 CI/私服/空缓存证据要求。

可定制目标产品、允许维护线和证据层级。输入不足时先给暂定组合，再列“缺少：版本约束；补充方式：提供 POM 与工具版本”。

## 常见问题

1. **是否总选最新版？** 不，先看约束。
2. **只选 ddd4j 版本够吗？** 不够，要完整元组。
3. **分支名能证明框架版本吗？** 不能。
4. **本地 SNAPSHOT 算可用吗？** 不算远端可用。
5. **CI 未启动怎么办？** 标 BLOCKED。
6. **矩阵过期怎么办？** 刷新当前 POM和验证脚本。
