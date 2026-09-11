# Subject 生命周期

1. 请求入口认证。
2. Provider 构造 ddd4j Subject。
3. Web/Runtime 绑定 ThreadContext 或请求作用域。
4. 应用层只读取 Subject/SubjectKit。
5. finally/作用域关闭恢复旧上下文。
6. 退出、异常、异步和线程复用均测试。

禁止把前一个请求的 Subject 泄漏到后一个请求。

