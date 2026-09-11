---
name: ddd4j-auth
description: Use when choosing, integrating, or reviewing ddd4j authentication and authorization with Sa-Token, Apache Shiro, or Spring Security, including Subject mapping, roles, permissions, sessions, temporary tokens, and exception handling.
license: Apache-2.0
---

# ddd4j Auth

## Overview

三种框架都映射为 ddd4j 的 Subject/AuthPrincipal/SubjectProvider；领域和应用代码不直接绑定具体安全上下文。

## 框架选择

| 场景 | 推荐 |
|---|---|
| 多账号、临时 Token、国内轻量项目 | Sa-Token |
| 已有 Realm/Subject/Permission | Shiro |
| Spring 企业安全、OAuth2/OIDC、方法安全 | Spring Security |

## 统一链路

认证框架→SubjectProvider→ddd4j Subject→AuthPrincipal→请求 Context→应用/领域服务。

每种实现必须说明依赖、配置、身份映射、角色权限、异常、上下文清理和测试。

## 能力边界

### ✅ 擅长

- Subject/AuthPrincipal/Provider 抽象。
- Sa-Token、Shiro、Spring Security 选择和使用。
- 临时 Token、API Key、角色权限。
- 请求生命周期和异常映射。

### ⚠️ 需要素材

- 当前维护线、运行时和认证框架。
- Token/Session 模式和账号体系。
- 角色、权限、租户与注销要求。

### ❌ 超范围

- 绕过认证或操作他人账号。
- 把 Same-Token 当最终用户 Token。
- 在领域层读取 SecurityContext/StpUtil/Shiro SecurityUtils。

## 工作流

1. 选择框架并确认实际 artifact。
2. 定义 AuthPrincipal profile、roles、permissions。
3. 实现/装配 SubjectProvider。
4. 在请求开始绑定，结束时恢复/清理。
5. 转换框架异常为稳定 Web 错误。
6. 测试匿名、合法、过期、角色不足、线程复用和注销。

## 常见错误

- 三框架同时装配并争夺 SubjectProvider。
- 硬编码 Sa-Token extra key。
- SecurityContext/Shiro Subject 未清理。
- 只测 login 成功，不测请求结束。
- 记录完整 Token/API Key。
- BOM 引入被当作认证已启用。

## 输出与异常

输出框架选择、artifact、配置、Subject 映射、生命周期和测试。缺失时写“缺少：认证框架/模式/运行时；补充方式：提供 POM 与脱敏配置”。

## 深度参考

- [框架选择](references/framework-selection.md)
- [Sa-Token](references/satoken.md)
- [Shiro](references/shiro.md)
- [Spring Security](references/spring-security.md)
- [生命周期](references/subject-lifecycle.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

仅使用虚构身份；Token、API Key、Session、组织和角色数据必须脱敏。
## 快速开始

- “使用 `$ddd4j-auth` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-auth` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-auth` 给出实现选择、证据状态和剩余风险。”

## 受众与定制

- 开发者：提供目标维护线、POM、功能和验收行为。
- 架构师：指定只读边界审查、兼容性或迁移目标。
- 测试/发布人员：指定所需证据层级，不自动扩大到发布或生产操作。

可定制目标框架、允许实现、排除模块、兼容性要求和输出证据层级。输入不足时先给暂定判断，再列出“缺少：具体项；补充方式：所需路径或配置”。

## 常见问题

1. **是否按 Maven artifact 创建技能？** 不，按用户面对的功能域组织。
2. **是否能直接套用其他维护线？** 不能，先核对版本和源码。
3. **源码中有类就表示能力可用吗？** 不表示，还需注册和行为证据。
4. **测试未运行如何报告？** 标记 NOT RUN 或 BLOCKED。
5. **可以自动提交或发布吗？** 只有用户明确授权后才执行。
6. **找不到实现怎么办？** 说明缺失的模块或证据，不编造 API。
