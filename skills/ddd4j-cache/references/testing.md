# 测试

1. 本地 provider：TTL、容量、invalidate、并发。
2. Redis/Memcached：真实容器 round-trip 和断连。
3. CAS：多客户端竞争。
4. 序列化：round-trip、损坏数据、版本变化。
5. 观测：hit/miss/error 与业务状态一致。

Docker 不可用或容器 skip 必须标记 BLOCKED/SKIPPED。
