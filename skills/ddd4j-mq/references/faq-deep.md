# 深度 FAQ

1. **MQClient 是 Broker 客户端吗？** 是统一端口，具体 adapter 实现。
2. **ACK 能自动吗？** 取决于 adapter/配置，需测试。
3. **失败一定 requeue 吗？** 由策略决定。
4. **Outbox 属于 MQ 吗？** 存储在 data，解决可靠发布。
5. **NATS 使用什么模式？** 核对 Core/JetStream 当前实现。
6. **SQS 有 topic 吗？** 语义不同，不机械套用。
7. **RocketMQ 名称限制？** 需要合法字符转换。
8. **ONS/TDMQ 能容器测吗？** 托管服务需明确替代/排除。
9. **Spring Cloud Stream 在哪？** ddd4j-cloud-stream 负责 Binder。
10. **完成证明是什么？** 真 Broker round-trip、可靠性和生命周期测试。
