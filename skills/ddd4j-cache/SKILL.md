---
name: ddd4j-cache
description: Use when choosing, configuring, implementing, or reviewing ddd4j cache providers, local caches, Redis clients, JetCache, Memcached, TTL, locking, CAS, statistics, or cache-backed idempotency.
license: Apache-2.0
---

# ddd4j Cache

## Overview

先选择单机或分布式一致性语义，再选择实现。所有实现通过 core Cache/CacheManager/CasCache/AtomicCache 契约被上层使用。

## 实现选择

| 场景 | 实现 |
|---|---|
| 单 JVM 高性能 | Caffeine、Guava、Hutool |
| Redis 原生客户端 | Lettuce、Jedis |
| 分布式锁/对象 | Redisson |
| 多级/统一抽象 | JetCache |
| Memcached | MemcachedCache |

## 核心规则

1. Caffeine/Guava/Hutool 不提供跨实例一致性。
2. 集群幂等需要共享原子 compare-and-set，而不只是分布式存储。
3. TTL 单位、零值、负值和精度必须按实现测试。
4. REDIS_OBJECT_MAPPER 只处理受信任缓存数据。
5. 锁必须有 owner、超时和异常释放。
6. CacheStats 不能代替业务成功指标。

## 能力边界

### ✅ 擅长

- 实现选择和配置。
- TTL、锁、CAS、统计。
- 本地与分布式语义。
- 幂等缓存后端评审。

### ⚠️ 需要素材

- 部署实例数和一致性目标。
- 缓存键/值、TTL、容量。
- Redis/Memcached/JetCache 运行环境。

### ❌ 超范围

- 把缓存当数据库。
- 宣称本地 Cache 支持集群幂等。
- 未授权清空生产缓存。

## 工作流

1. 定义数据权威和失效策略。
2. 选择 local/distributed/multilevel。
3. 验证 get/put/invalidate、TTL、并发和失败。
4. 若需幂等，验证真实 CAS 竞争。
5. 加入观测、容量和降级策略。

## 常见错误

- 多实例仍使用 Caffeine 幂等。
- get-then-put 冒充 CAS。
- 缓存 key 缺租户隔离。
- 反序列化不可信缓存内容。
- 锁异常路径未释放。
- Redis 不可用时静默返回成功。

## 深度参考

- [实现矩阵](references/provider-matrix.md)
- [CAS 与幂等](references/cas-and-idempotency.md)
- [序列化与键](references/serialization-and-keys.md)
- [测试](references/testing.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

缓存键、值和日志不得暴露 Token、密码、身份证、手机号或租户秘密。

## 快速开始

- “使用 `$ddd4j-cache` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-cache` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-cache` 给出实现选择、证据状态和剩余风险。”

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
