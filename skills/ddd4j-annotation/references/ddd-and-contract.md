# DDD 与契约注解

- Contract：标注其他注解是可审计契约。
- BusinessType：业务类型枚举/分类模型。
- DDDAnnotation：通用 DDD 元数据入口。

不要假设 DDDAnnotation 自动注册 Spring/CDI Bean。运行时融合由对应 Runtime 模块验证。
