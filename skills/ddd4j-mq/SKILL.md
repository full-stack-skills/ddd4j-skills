---
name: ddd4j-mq
description: Use when choosing, implementing, or reviewing ddd4j messaging with Kafka, RabbitMQ, Pulsar, RocketMQ, ActiveMQ, Artemis, MQTT, NATS, SQS, ONS, TDMQ, Redis Stream, Spring integration, acknowledgments, retries, dead letters, or lifecycle.
license: Apache-2.0
---

# ddd4j MQ

## Overview

所有 Broker 适配统一到 MQClient、MQListener、MQEvent、Acknowledgment；先选择交付和运维语义，再选择 Broker。

## Broker 路由

| 需求 | 候选 |
|---|---|
| 高吞吐日志/流 | Kafka |
| AMQP 路由 | RabbitMQ |
| 多租户流/队列 | Pulsar/TDMQ |
| 国内事务/顺序消息 | RocketMQ/ONS |
| JMS | ActiveMQ/Artemis |
| IoT | MQTT/Mica MQTT |
| 轻量 JetStream | NATS |
| AWS | SQS |
| Redis 基础设施 | Redis Stream |
| 进程内 | Disruptor |
| Spring Cloud | 由 Cloud Stream 适配统一 |

## 核心规则

1. required listener 初始化失败应阻止启动；optional 可降级 readiness。
2. 成功业务处理后 ack，失败按策略 nack/requeue。
3. 重试需 backoff、上限和 dead-letter。
4. message id/业务键用于幂等，不能只依赖 Broker。
5. 初始化部分失败要反向关闭已创建资源。
6. close 幂等；线程、consumer、producer、connection 均有 owner。
7. persist=true 等配置必须有行为测试。

## 能力边界

### ✅ 擅长

- Broker 选择和统一 API。
- ACK/NACK、重试、死信、幂等。
- 监听器扫描和生命周期。
- Testcontainers round-trip。

### ⚠️ 需要素材

- Broker、交付语义和顺序要求。
- topic/tag/group/namespace。
- 部署和容灾模型。

### ❌ 超范围

- 只启动容器就称消息链成功。
- 用 mock 证明 Broker durability。
- 把 topic 命名跨 Broker 机械统一。

## 工作流

1. 定义 at-most/at-least-once 和顺序。
2. 选择 Broker/adapter。
3. 配置 producer/consumer/listener。
4. 验证 publish→consume→ack。
5. 验证 retry/dead-letter/duplicate/recovery。
6. 验证启动回滚、readiness 和关闭。

## 常见错误

- ACK 在业务处理前完成。
- 消费失败被吞掉。
- required consumer 启动失败仍 READY。
- Broker 容器启动被当 round-trip。
- RocketMQ destination 使用非法字符。
- 测试 skip 被写成 PASS。

## 深度参考

- [Broker 矩阵](references/broker-matrix.md)
- [ACK 与可靠性](references/ack-retry-dead-letter.md)
- [生命周期](references/lifecycle.md)
- [测试](references/testcontainers.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

消息 payload、headers 和日志不得泄露 Token、PII、云访问密钥。

## 快速开始

- “使用 `$ddd4j-mq` 分析我当前项目应该采用的实现和配置。”
- “使用 `$ddd4j-mq` 对照当前源码审查现有用法。”
- “使用 `$ddd4j-mq` 给出实现选择、证据状态和剩余风险。”

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
