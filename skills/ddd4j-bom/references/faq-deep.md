# 深度 FAQ

1. **业务项目该继承 parent 还是导入 BOM？** 构建约定用 parent，仅版本用 BOM。
2. **dependencies 能直接给业务导入吗？** 按项目契约，通常 BOM 是稳定消费面。
3. **为什么适配器还有 BOM？** 管理生态专属 artifact 和框架版本。
4. **模块能写版本吗？** 只有所有权明确且上层未管理时。
5. **POM 4.1 能用 Maven 3 吗？** 不能作为受支持路径。
6. **3.0.x 为什么用 subprojects？** Maven 4 Model 4.1 契约。
7. **effective POM 通过等于运行通过吗？** 不等于。
8. **BOM 可解析等于 JAR 齐全吗？** 不等于。
9. **如何检查导入冲突？** 运行项目脚本并检查 effective POM/dependency tree。
10. **enforcer.skip 能用于发布吗？** 不能，只能是限定诊断证据。
