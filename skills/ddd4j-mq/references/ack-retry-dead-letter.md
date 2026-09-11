# ACK、重试和死信

- 业务成功且 acknowledgment open/未确认时 ack。
- 业务异常时 nack，并由策略决定 requeue。
- 重试记录 attempts、next attempt、last error。
- 超限进入 dead-letter。
- producer 发送与业务事务之间需要 Outbox 等可靠桥。
- consumer 按 message/event id 幂等。

