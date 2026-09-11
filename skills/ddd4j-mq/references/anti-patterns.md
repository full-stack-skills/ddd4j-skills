# 反模式

1. **容器即成功**：只启动 Broker；要求 round-trip。
2. **提前 ACK**：业务前确认；成功后确认。
3. **无限重试**：无 backoff/dead-letter；设上限。
4. **关闭泄漏**：只关 consumer；逆序关闭全部 owner。
5. **命名通吃**：跨 Broker 复用非法 destination；按规则转换。

