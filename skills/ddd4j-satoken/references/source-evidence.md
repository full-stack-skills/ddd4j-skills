# 源码证据索引

- `ddd4j-auth-satoken/.../util/StpKit.java`：DEFAULT/ADMIN/USER 与扩展类型转换。
- `.../util/SaTempKit.java`、`SaTempToken.java`：临时凭证生命周期。
- `.../util/ApiKeyKit.java`：API Key。
- `.../subject/SaTokenSubject*.java`：ddd4j Subject 桥。
- `.../config/SaTokenSecurityProperties.java`、`SaTokenAuthenticationMode.java`：配置。
- `.../handler/SaMixCheckLoginHandler.java`、`SaInternalCheckHandler.java`：注解处理。
- 对应测试目录覆盖配置、handler、Subject 和工具。

使用时以当前 Sa-Token 版本和目标运行时为准。
