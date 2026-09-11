# 反模式

1. **凭印象写 API**：AllowedValues(values=...)；按源码使用 AllowableValues(allows=...)。
2. **把格式化当校验**：只加 DateTimeFormat；使用约束并测试。
3. **忽略 null**：Number/Phone validator 直接处理 value；明确非空组合。
4. **把输入校验当领域不变量**：DTO 通过后聚合不再校验；两层各负其责。
5. **跨线机械复制**：Jakarta import 复制到旧线；逐线编译。
