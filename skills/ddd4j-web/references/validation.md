# Validation

公开约束：AllowableValues(allows, nullable)、PhoneNumber(lang)、NumberValue(regex)、StringDateValue(pattern)。

StringDateValue 当前空文本通过且严格日期解析；Number/Phone 的 null 行为需配合 NotNull 和测试。3.0.x 使用 jakarta.validation，旧线逐线确认。

