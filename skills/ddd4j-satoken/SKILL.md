---
name: ddd4j-satoken
description: Use when integrating current ddd4j-auth-satoken with StpKit account systems, SaTokenSubject bridging, authentication modes, internal/mixed login handlers, temporary tokens, API keys, or Javalin/Spring runtime adapters.
license: Apache-2.0
---

# ddd4j Sa-Token

## Overview

把 Sa-Token 会话适配为 ddd4j 的 `Subject` 与认证 SPI。通用 login/permission API 仍属于 Sa-Token；本技能只处理 `io.ddd4j.auth.satoken` 封装。

## 快速开始

- “使用 StpKit.USER/ADMIN 多账号体系。”
- “把 Sa-Token 当前会话转换为 ddd4j Subject。”
- “配置 SaTokenAuthenticationMode。”
- “创建并校验 SaTempToken 或 API Key。”

## 受众、路由与定制

- 认证开发者：指定账号体系、认证模式、Subject 映射和运行时。
- 安全审查者：指定 Token/API Key/内部调用与撤销边界。
- 集成开发者：指定 Javalin、Spring 或其他适配器。
- 通用 Sa-Token 问题：转用 sa-token 技能，不假定 ddd4j 封装。

输入不足时先给出当前封装入口，再输出“缺少：账号体系/模式/TTL/运行时；补充方式：提供脱敏配置与目标行为”。

## 能力边界

### ✅ 擅长

1. `StpKit.DEFAULT/ADMIN/USER` 与类型安全扩展读取。
2. `SaTokenSubject`、`SaTokenSubjectDataBridge`、`SaTokenSubjectProvider`。
3. `SaTokenSecurityProperties/Configurer` 与认证模式。
4. `SaMixCheckLogin`、`SaInternalCheck` 处理器。
5. `SaTempKit`、`SaTempToken` 和 `ApiKeyKit`。

### ⚠️ 需要素材

1. 当前维护线与 Sa-Token 版本。
2. 账号体系、Token 模式、Subject 字段和运行时。
3. 临时 Token/API Key 的业务标识、TTL 与撤销要求。

### ❌ 超范围

1. 通用 Sa-Token 教程。
2. 硬编码 `"uuid"`、`"orgId"` 等扩展键。
3. 把临时 Token 当成长期会话或跳过权限检查。

## 快速参考

| 目标 | 当前入口 |
|---|---|
| 默认账号 | `StpKit.DEFAULT` |
| 管理员/用户 | `StpKit.ADMIN` / `StpKit.USER` |
| 用户/组织信息 | `StpKit.getUserId*()/getOrgId*()` 等封装 |
| ddd4j Subject | `SaTokenSubjectProvider` |
| 临时 Token | `SaTempKit.createToken(...)` 返回/解析 `SaTempToken` |
| API Key | `ApiKeyKit` |
| 认证模式 | `SaTokenAuthenticationMode` |

## 示例

```java
StpKit.USER.login(userId);
Long currentUserId = StpKit.getUserIdAsLong();

SaTempToken temp = new SaTempToken();
temp.setLoginId(String.valueOf(userId));
String token = SaTempKit.createToken(temp, 300);
SaTempToken verified = SaTempKit.checkTempToken(token);
```

具体重载以当前 `SaTempKit` 源码为准；不要沿用旧的 `createToken(userId, 300)` 假签名。

## 工作流

1. 确认账号体系、JWT/会话模式和运行时适配器。
2. 使用 `AuthConstants`/封装 getter 读取扩展数据。
3. 通过 Subject bridge 暴露 ddd4j 身份，不在领域层依赖 Sa-Token。
4. 为匿名、过期、错误账号体系、内部调用和撤销编写测试。
5. 临时 Token/API Key 明确 TTL、用途、撤销和重放边界。

## 常见错误

- 业务代码散落 `StpUtil.getExtra("uuid")`。
- 默认 StpLogic 与 USER/ADMIN 混用。
- 假设扩展数据在所有 Token 模式下一致。
- 把 Same-Token 当最终用户 Authorization。
- 日志打印完整 Token/API Key。
- 只验证 Token 存在，不验证 Subject、权限和账号体系。

## 输出与异常

说明账号体系、认证模式、Subject 映射、TTL、撤销与测试结果。缺少时输出“缺少：账号体系或 Token 模式；补充方式：提供安全配置和目标运行时”。

## 隐私与安全

所有示例使用虚构身份；Token、API Key、会话扩展、组织和角色信息必须脱敏。不得绕过权限或操作他人账号。

## FAQ

1. **为何不用 StpUtil 直接读取所有字段？** ddd4j 封装提供稳定键和类型转换。
2. **Subject 是否等于 StpLogic？** 不等于，Subject 是 ddd4j 框架无关身份。
3. **临时 Token 能长期使用吗？** 不能，应短 TTL、单一用途并支持撤销。
4. **Same-Token 是用户登录 Token 吗？** 不是，它用于服务间身份边界。
5. **能记录 Token 排障吗？** 只能记录脱敏指纹和非敏感元数据。
6. **怎样证明集成正确？** 配置、handler、Subject 生命周期和失败路径测试共同证明。

## 深度参考

- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)
