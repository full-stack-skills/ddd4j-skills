# 深度 FAQ

1. **allows 如何分隔？** 当前 Spring tokenizeToStringArray 按逗号。
2. **nullable=true 包括空白吗？** 当前用 StringUtils.hasText，空白可放行。
3. **NumberValue 接受 null 吗？** 当前实现可能在 matcher 处失败，需配合非空约束并测试。
4. **PhoneNumber 判断有效还是可能？** 当前使用 isPossibleNumber。
5. **PhoneNumber.value 有作用吗？** 当前 Validator 未使用。
6. **StringDateValue 空串如何处理？** 当前返回 true。
7. **日期解析严格吗？** setLenient(false)，但还应测试尾随字符等完整消费。
8. **message 必须设置吗？** Number/Phone/Date 无默认值，编译时必填。
9. **AllowableValues 有默认 message 吗？** 有 `invalid values`，生产建议显式国际化消息。
10. **该模块是否纯 Bean Validation？** 当前 Validator 还依赖 Spring StringUtils。
