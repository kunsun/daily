# rc-form架构解析

* mapPropsToFields(props) :  把props属性映射到表单项上，需要对返回值中的表单数据用Form.createFormField标记，注意表单项将变成受控组件，error等也需要一并手动传入
* onFieldsChange :  当表单数据值发生变化时触发，可以把对应的值转存到Redux store
* Form.createFormField :  标记成Field

###一、createBaseForm

* createBaseForm(options, mixins) : 
  * options，用于配制表单层面的绑定函数，检验文案以及部分字段组件的props属性名: 
    * mapPropsToFields(props)
    * onFieldsChange(props, fields)
  * mixins，将作为实例方法混入BaseForm，其中createDomForm函数即通过这一机制混入了vlidateFieldAndScroll方法：
    * getFieldProps(name, fieldOption)：字段组件的渲染。
      * 用于为FieldsStore实例收集字段的元数据
      * 指定字段组件的ref引用函数
      * 为字段组件绑定onCollect，onCollectValidate实例方法，以在指定事件触发时收集或校验字段的值
      * 最终将输出注入字段组件的props，包含所有的元数据与实时数据
    * getFiledDecorator(name, fieldOption)：字段组件的渲染。直接装饰字段组件，这样就可以操控添加在字段组件上的ref引用函数及props.onChange等绑定函数

### 二、FieldStore

1. 在用户行为驱动字段变更时，即时储存字段的值及校验信息，继而调用表单组件实例的forceUpdate方法强制重绘
2. 在绘制过程中，再从FieldStore实例读取实时数据及校验信息

#### 数据结构

* fileds：以fields属性储存表单的实时数据，即由用户行为或者开发者显示更新的数据。把实时数据已存入fields中的字段称为已收集字段；反之，称为未收集字段。
  * value
  * errors
  * validating：校验状态
  * dirty：为true说明字段值已变化，但未做校验，所以可以说脏数据就是未做校验的数据。
  * touched： 用户的标识，为true说明用户行为使字段的值发生了变化
* filedsMeta：储存字段的元数据
  * validate
  * hidden
  * getValueFromEvent(event)
  * initialValue：字段的初始值。当字段未做收集时，初始值用作字段的值
  * valuePropName
  * getValueProps(value)
  * normalize(newValue, oldValue, values)：用于转化存入FieldsStore实例的字段的值





