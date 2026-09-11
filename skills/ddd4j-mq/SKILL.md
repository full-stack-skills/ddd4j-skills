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

