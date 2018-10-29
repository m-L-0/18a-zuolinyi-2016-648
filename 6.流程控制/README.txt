1.比较运算OP
tf.equal  x == y
tf.not_equal  x != y
tf.less  x < y
tf.less_equal  x <= y
tf.greater  x > y
tf.greater_equal  x >= y
tf.where特殊的比价运算符，根据判别条件，分别从两个张量中抽取任意子元素组成新的向量。
返回true的位置，抽取子元素组成新元素
'input' tensor is [[True, False]
             [True, False]]
'input' has two true values, so output has two coordinates.
'input' has rank of 2, so coordinates have two indices.
where(input) ==> [[0, 0],
             [1, 0]]
`input` tensor is [[[True, False]
              [True, False]]
             [[False, True]
              [False, True]]
             [[False, False]
              [False, True]]]
'input' has 5 true values, so output has 5 coordinates.
'input' has rank of 3, so coordinates have three indices.
where(input) ==> [[0, 0, 0],
             [0, 1, 0],
             [1, 0, 1],
             [1, 1, 1],
             [2, 1, 1]]
             
2.张量拷贝
tf.idnetity适用于创建张量副本的虚节点，即生成一个与输入张量相同shape与元素的新张量。
tf.identity(inputs, name)

3.张量结组
tf.group可以用于将一系列op、tensor组合成为一个op，方便统一操作，没有返回值。
(1)双分支选择结构
tf.cond构建选择结构。
tf.cond(condition, true_fn, false_fn, strict, name)

4.多路分支选择结构
写成多个二分支结构的等价形式。
一般的多路分支选择结构使用tf.case来实现。

5.循环结构
使用tf.while_loop构建。
tf.while_loop(cond 循环条件, body 循环执行内容, loop_vars 两个函数的参数列表)