# CAS 与幂等

core 提供 AtomicCache、CasCache、CASOperation、GetsResponse。

集群幂等测试至少包含：两个独立客户端竞争同一 key、单一成功者、TTL 后再获取、网络失败、重试不重复提交。本地同步或单 JVM测试不能证明跨实例 CAS。
