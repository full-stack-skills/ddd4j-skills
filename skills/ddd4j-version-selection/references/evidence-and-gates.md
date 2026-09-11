# 证据与门禁

## 状态层级

1. SOURCE：POM、矩阵、源码存在。
2. TEST：目标构建/行为测试实际执行。
3. CI：最终 SHA 的必需 job 终态成功。
4. PUBLISHED：完整 deploy 零退出且远端元数据完整。
5. CONSUMED：隔离空缓存从私服解析和编译。
6. PRODUCTION：真实部署和运行验收。

不得用较低层级替代较高层级。

## 选择前检查

- git branch --show-current
- git status --short --branch
- java -version
- ./mvnw -version
- 根 POM modelVersion、revision、java.version
- 适配项目 framework/BOM 版本
- CI 与私服目标坐标

## 当前采集 SHA

| 仓库/线 | SHA |
|---|---|
| ddd4j 1.0.x | d9149cb0371cf24328822c17596a408bde3562a5 |
| ddd4j 2.0.x | bbf3dfa330c083ccccafdfe1ac2c266a74513a27 |
| ddd4j 3.0.x | 0699b19917575ebd263182d0fc43457b1aff56db |
| ddd4j-boot 4.1.x | 2c41353821b9c4c027a16da71dad7af0d8edb9c2 |
| ddd4j-javalin 6.7.x checkout | 36865c0935c7af3148c98901da62966e60b6be3d |
| ddd4j-quarkus 4.0.x checkout | e899da7e6eecd4d39320982c0141d29f48028915 |
| ddd4j-cloud 2024.0.x | a3a11af917b221d63ebad3c2481e85b7cb2ed270 |

这些 SHA 只证明采集时来源，使用时必须刷新。

