---
name: ddd4j-bom
description: Use when choosing or changing ddd4j parent, dependencies, BOM imports, Maven model, version ownership, dependency properties, release-line alignment, or consumer dependency management.
license: Apache-2.0
---

# ddd4j BOM 与 Maven 治理

## Overview

Parent 管构建，dependencies 管第三方版本，BOM 管 ddd4j 消费坐标。三者职责不同；适配项目 BOM 只拥有自身生态版本。

## 快速选择

| 需求 | 使用 |
|---|---|
| 插件、编译、发布默认值 | ddd4j-parent |
| 第三方 dependencyManagement | ddd4j-dependencies |
| 业务消费者导入 ddd4j 模块版本 | ddd4j-bom |
| Boot/Javalin/Quarkus/Cloud 专有版本 | 对应适配项目 dependencies/BOM |

## 核心规则

1. 1.0.x/2.0.x 保持 POM 4.0/Maven 3；3.0.x 使用 POM 4.1/Maven 4。
2. POM 4.0 使用 modules/module；4.1 使用 subprojects/subproject。
3. 具体模块不重复固定已由 dependencies 管理的第三方版本。
4. ddd4j-dependencies 是普通平台依赖权威。
5. Boot/Cloud/Javalin/Quarkus BOM 只管理生态表面。
6. 导入 BOM 的顺序会影响有效版本，必须检查 effective POM。
7. parent/BOM 可解析不代表全部 JAR 已发布。

## 能力边界

### ✅ 擅长

- Parent、Dependencies、BOM 职责选择。
- Maven 3/4 与 Model 4.0/4.1。
- 属性布局、版本泄漏和导入冲突。
- 多维护线依赖对齐和消费验证。

### ⚠️ 需要素材

- 当前维护线与 JDK/Maven。
- 目标 POM和 effective POM。
- 私服/中央仓库解析结果。

### ❌ 超范围

- 静默改版本或发布。
- 用 enforcer.skip 作为发布证明。
- 仅靠 XML关键词判断所有权。

## 验证门禁

- scripts/test_maven4_model_contract.py
- scripts/test_dependency_property_layout.py
- scripts/test_bom_import_conflicts.py
- scripts/test_dependency_alignment.py
- scripts/check-bom-alignment.sh
- 空缓存 consumer 的 dependency:go-offline/compile

## 常见错误

- BOM 与 parent 混用。
- 在具体模块散落数字版本。
- Maven 4 聚合 POM保留 modules。
- 只看 source POM，不看 effective POM。
- 上传部分模块后宣称全量发布。
- 私服热缓存掩盖缺失 parent/BOM。

## 输出与异常

输出维护线、JDK、Maven、POM Model、版本所有者、effective POM 和消费状态。缺失时写“缺少：有效模型/远端坐标；补充方式：执行 help:effective-pom 或空缓存解析”。

## 深度参考

- [职责与导入](references/ownership-and-imports.md)
- [Maven Model](references/maven-model.md)
- [发布消费](references/publication-and-consumption.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得打印 settings.xml、服务器密码或私服 Token。

