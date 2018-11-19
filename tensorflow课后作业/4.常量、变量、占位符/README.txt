1.常量
（1）常量用tf.constant()初始化得到。
constant(value, dtype=None, shape=None, name="Const", verify_shape=False)
value是必填参数
（2）生成序列常量：tf.linspace(start, stop, num),tf.range(start, limit, delta)
（3）生成随机数常量：
服从正态分布的随机数tf.random_normal()
服从均匀分布的随机值rf.random_uniform()
（4）随机数种子
图级种子:tf.set_random_seed()
（5）特殊常量
tf.zeros(shape,dtype,name)
tf.zeros_like(tensor,dtype,name)
tf.ones(shape,dtype,name)
tf.ones_like(tensor,dtype,name)
tf.fill(dims,value,name)
2.变量
（1）tf.Variable()实例化一个变量对象
例：var = tf.Variable([1, 2, 3])
（2）tf.get_variable()创建变量
tf.get_variable(name= 'get_var',shape=[3, ])
（3）变量初始化
var = tf.Varaible([1,2,3])
with tf.Session() as sess:
    sess.run(var.intializer)
    print(sess.run(var))
（5）变量赋值
a = tf.Variable([1,2,3])
with tf.Session() as sess:
    sess.run(tf.global_variables_initializer())
    print(sess.run(a))
    
    sess.run(tf.assign(a,[2,3,4]))
    print(sess.run(a))
    
    sess.run(a.assign([2,3,4]))
    print(sess.run(a))
3.占位符和feed_dict
tf.placeholder(dtype,shape,name)
x = tf.placeholder(dtype = tf.float32,shape=[])
y = tf.placeholder(dtype = tf.float32,shape=[])
z = tf.multiply(x, 2) +y
with tf.Session() as sess:
    sess.run(z,feed_dict={x:1,y:2})