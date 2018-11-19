1.使用tf.io.read_file()可根据filename将数据读出来，之后可使用相关的解码操作解码出数据。
f = tf.io.read_file('test.png')
decode_img = tf.image.decode_png(f, channels=4)
使用tf.io.write_file()写入文件。
tf.io.write_file('new.png', f)

2.解码数据
使用tf.io.decode_raw解码张量数据

3.gfile模块-文件操作模块
（1）打开文件流
tf.gfile.GFile或者tf.gfile.Open
tf.gfile.FastGFile支持无阻塞的读取。

可读、写、创建文件
with tf.gfile.GFile('test.txt','w+') as f:

可以给test.txt追加内容
with tf.gfile.Open('test.txt','a') as f:

只读test.txt
with tf.gfile.FaseGFile('test.txt','r') as f:

操作二进制格式的文件
with tf.gfile.FastGFile('test.txt','wb+') as f:

4.数据读取
文件读取时，会有一个指针指向读取的位置，当调用`read`方法时，就从这个指针指向的位置开始读取，调用之后，指针的位置修改到新的未读取的位置。

tf.gfile.FasrGFile.read(n = -1)
n = -1,代表读取整个文件，n != -1,代表读取n个bytes长度

使用readline方法对文件进行读取，可以读取以\n为换行符的文件的一行内容。
f.readline()
f.readlines() = [line for line in f]
读取下一行内容。
f.next()

5.其他文件操作