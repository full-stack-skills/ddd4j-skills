# 反模式

1. **Domain 即 PO**：框架注解污染聚合；显式映射。
2. **假事务**：EventStore/Outbox 独立提交；共享事务入口。
3. **并发位置冲突**：MAX+1；使用原子 allocator。
4. **投影丢失**：先 cursor 后 view；保证提交顺序。
5. **数据库假绿**：仅 H2/mock；真实方言容器。
