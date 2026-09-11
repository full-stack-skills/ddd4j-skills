# Apache Shiro

入口：ShiroSubject、ShiroSubjectProvider。

- 从当前 Shiro Subject 映射 principal、roles、permissions。
- 无绑定 Subject 时返回明确匿名/空主体语义。
- Realm 和 SessionManager 属于运行时配置，不放进领域层。
- 线程池和请求结束必须解除 Shiro ThreadContext。
- 用 ShiroSubjectProviderTest/ShiroSubjectTest 校正行为。

