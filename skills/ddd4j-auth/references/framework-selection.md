# 框架选择

| 维度 | Sa-Token | Shiro | Spring Security |
|---|---|---|---|
| 当前模块 | ddd4j-auth-satoken | ddd4j-auth-shiro | ddd4j-auth-security |
| 统一出口 | SaTokenSubjectProvider | ShiroSubjectProvider | SecuritySubjectProvider |
| 原生上下文 | StpLogic | Shiro Subject | SecurityContextHolder |
| 强项 | 多账号/临时 Token | Realm/权限模型 | Spring/OAuth2/OIDC |
| 主要风险 | 账号体系混用 | ThreadLocal 清理 | Filter/Context 生命周期 |

选定一个主 SubjectProvider；多框架共存必须显式定义优先级。

