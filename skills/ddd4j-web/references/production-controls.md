# 生产控制

- Idempotency：单实例 local 与生产 shared CAS 分开。
- CORS：origin/credentials/headers/methods allowlist。
- Limits：request size、timeout、rate limit。
- Health：liveness 只看进程；readiness 聚合 DB/MQ/Auth/Outbox 等 required dependency。

