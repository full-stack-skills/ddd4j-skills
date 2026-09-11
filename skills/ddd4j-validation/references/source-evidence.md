# 源码证据索引

- `ddd4j-web-validation/.../constraints/AllowableValues.java`
- `.../constraints/PhoneNumber.java`
- `.../constraints/NumberValue.java`
- `.../constraints/StringDateValue.java`
- `.../constraintvalidators/AllowedValuesValidator.java`
- `.../constraintvalidators/PhoneValueValidator.java`
- `.../constraintvalidators/NumberValueValidator.java`
- `.../constraintvalidators/StringDateValueValidator.java`

3.0.x 当前使用 `jakarta.validation`。AllowableValues 用逗号分隔的 `allows`；StringDateValue 属性名是 `pattern`；PhoneNumber 的 `value` 当前未参与 Validator 逻辑。
