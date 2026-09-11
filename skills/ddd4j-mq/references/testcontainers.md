# Testcontainers

测试至少覆盖：容器可达、真实 publish/consume、header、ack、nack/retry、duplicate、recovery、close。

优先官方 Testcontainers module；无官方模块时使用有界 GenericContainer。Docker 不可用标 BLOCKED/SKIPPED，不是 PASS。
