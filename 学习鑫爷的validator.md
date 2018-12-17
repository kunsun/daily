# validator

验证器，用来验证表单的格式

## 字段

### validatorConfig

验证规则object

{字段: [规则1， 规则2]}

### allValidKeys

所有需要验证的字段数组

[字段1，...]

### err

目前错误的字段对象

{字段：' '，}

## 方法

### validator

```js
// 返回
{ valid: boolean, errs: ['错误1', '错误2']}
```





