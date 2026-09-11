# API 与 CQRS 注解

## API

- ApiIdempotent / ApiIdempotentType：声明幂等策略，行为由 Web guard 实现。
- ApiModule：API 模块元数据。
- ApiOperationLog：操作日志元数据。
- RawResponse：跳过统一响应包装的意图。

## CQRS

- CreateEvent、UpdateEvent、DeleteEvent：方法级事件意图。

每项都要追踪实际扫描器/拦截器；注解存在不是行为证据。
