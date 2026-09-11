# Spring Security

入口：SecuritySubject、SecuritySubjectProvider、AuthUserDetails、SecurityExceptionHandler。

- 从 SecurityContextHolder Authentication 映射 AuthPrincipal。
- 区分 unauthenticated、anonymous 和已认证。
- GrantedAuthority 到 role/permission 的映射必须明确。
- 请求结束由 Security filter chain 清理，异步传播需单独配置。
- OAuth2/OIDC 是 Spring Security 配置，不自动等于 ddd4j Subject 已注册。

