# Outbox 与事务

1. 业务写、领域事件和 Outbox 行在同一事务。
2. Relay 原子 claim。
3. 发送成功后 confirm。
4. 失败 backoff/retry。
5. 超限 dead-letter。
6. 消费/发布以 event/message id 幂等。
7. 崩溃恢复测试覆盖 claim 后、send 后、confirm 前窗口。

