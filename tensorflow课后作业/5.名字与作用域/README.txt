1.所有的tensor、operation均有name属性，是其唯一的标识符。使用name可是使得tensorflow使用某一个编程语言编写的图在其他语言中方便操作，实现跨语言环境的兼容，也有助于可视化。
作用域scope，用来管理tensor，operation的name和完成一些可复用的操作。tensorflow的作用域有两种，variable_scope,name_scope。

2.nanme
（1）只能给operation进行主动命名，tensor的name由operation根据自己的name与输出数量进行命名。
a = tf.constant([1, 2, 3], name = 'const')
给op定义了一个name为const，a是op的输出值，a的名字是const:0
(2)tensor的name构成
生成此tensor的op的name，冒号，op输出内容的索引默认从0开始
key, value = tf.ReaderBase.read(...,name = 'read')
print(key.name) # read:0
print(value.name) #read:1
（3）op与tensor的默认name
（4）重复name的处理方式
tensorflow并不会强制要求我们必须设置完全不同的name
当出现了两个op设置相同的name时，tensorflow会自动给后面的op的name加一个后缀，后缀由下划线与索引组成，索引从1开始。
    ma_add:0
    ma_add_1:0
当不指定name时，使用默认的name也是相同的处理方式。
不同操作之间有相同的name也是如此处理。
（5）不同图中相同操作name
两个图中有相同的操作或者相同的name时，并不会互相影响。

3.通过name获取op与tensor
tf.Graph.get_tensor_by_name方法可以根据name获取tensor，返回值是一个tensor对象。
tf.Graph.get_operation_by_name方法获取op。
在会话中，fetch一个tensor，返回一个tensor，fetch一个op，返回一个none

4.name_scope
(1)name_scope可以为其作用域中的节点的name添加一个或多个前缀，并使用这些前缀作为划分内部与外部op范围的标记。name_scope可以嵌套使用，代表不同层级的功能区域的划分。
name_scope使用tf.name_scope()创建。
tf.name_scope(name, default_name, values)
例：
a = tf.constant(1, name = 'const')
print(a.name) #const:0
with tf.name_scope('scope_name') as name:
    print(name) #scope_name
    b = tf.constant(1, name = 'const')
    print(b.name) #scope_name/const:0
在一个name_scope的作用域中，可以填写name相同的op，但tensorflow会自动加后缀。
    scope_name/const:0
    scope_name/const_1:0
(2)多个name_scope
可以指定任意多个name_scope，并且可以填写相同name的两个或多个name_scope，但tensorflow会自动给name_scope的name加上后缀。
    scope_name/
    scope_name_1/
(3)多级name_scope
`name_scope`可以嵌套，嵌套之后的`name`包含上级`name_scope`的`name`
例：
with tf.name_scope('name1'):
    with tf.name_scope('name2') as name2:
        print(name2)  #name1/name2/
（4）注意事项
从外部传入的`Tensor`，并不会在`name_scope`中加上前缀
不推荐使用/

5.variable_scope
variable_scope主要用于管理变量作用域以及变量相关的操作，也可以用来给不同操作区域划分范围，可以与tf.get_variable()等配合使用完成对变量的重复使用。
（1）给op的name加上name_scope
vaiable_scope可以给op与tensor加上name_scope.
(2)同名variable_scope
创建两个或多个variable_scope时可以填入相同的name，相当于创建了一个variable_scope与两个或多个name_scope。
(3)get_variable()的用法
使用tf.get_variable()函数创建于获取模型的变量。
tf.gat_variable(name, dtype, shape)
tf.get_variable()必须提供一个独一无二的name，不能重复。
(4)多级变量作用域
变量作用域是可以嵌套使用的，其name前缀也会嵌套。












































