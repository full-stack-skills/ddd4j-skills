# Context 与错误

传播 Request ID、Trace ID、Tenant、Subject；入口绑定，finally/异步完成时恢复。区分 400、401、403、404、409、415、422、429、500。统一载荷不能吞 cause，也不能暴露内部堆栈。

