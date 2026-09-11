# 生命周期

validate→initialize→register→ready→drain→close。失败时只关闭已完成初始化的资源，逆序执行。close 可重复调用。请求 scope 在成功、异常和异步完成时恢复。

