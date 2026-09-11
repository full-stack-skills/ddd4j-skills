# Maven Model

| ddd4j 线 | JDK | Maven | model | 聚合 |
|---|---:|---|---|---|
| 1.0.x | 8 | 3 | 4.0.0 | modules |
| 2.0.x | 17 | 3 | 4.0.0 | modules |
| 3.0.x | 21 | 4 | 4.1.0 | subprojects |

运行 scripts/test_maven4_model_contract.py 验证模型规则。不要为了统一格式破坏旧线工具链。

## 当前验证注意事项

2026-09-11 在当前 3.0.x 检出执行该测试时，`verify_owned_source` 还扫描了
`.superpowers/sdd/.../task-4-baseline-2` 中的历史基线 POM，导致
`test_repository_has_no_owned_warning_sources` 报告 relocated Quarkus test artifact。
这属于验证范围污染：在修复脚本排除规则或改用干净检出前，Maven 4 owned-source
门禁必须标记为 BLOCKED，不能写成 PASS。
