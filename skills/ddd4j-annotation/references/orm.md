# ORM 注解

- DomainField：Domain 字段与 PO 属性/列映射。
- BizKey：业务键。
- TenantId/SystemId：隔离字段。
- OnCreate/OnUpdate：审计填充。
- OrderBy：默认排序元数据。

验证链：注解→DomainModelInfo/TableInfo→Repository/Interceptor→真实数据库行为。
