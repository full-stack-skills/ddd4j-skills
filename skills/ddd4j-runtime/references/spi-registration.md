# SPI 注册

Contexts/Registry/SubjectKit 等静态入口必须由 runtime 注册。注册要检测重复和缺失，并用作用域对象恢复之前的值。CommandBus 重复 executor 类型应 fail-fast。

