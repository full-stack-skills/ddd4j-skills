# Projection 指标

核心端口：ProjectionMetrics/NoopProjectionMetrics。实现：OpenTelemetryProjectionMetrics。

至少记录 run success/failure、processed events、duration、position lag（若有可靠来源）。异常路径仍记录 failure，且不推进伪成功状态。
