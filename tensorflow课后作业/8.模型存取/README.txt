一.图存取
1.图的保存
第一步：获取图定义
tf.Graph.as_garph_def方法
第二步：保存图的定义
直接将图存为文本文件
使用tensorflow提供的专门的保存图的方法
tf.train.write_graph(
    graph_or_graph_def,
    logdir,
    name,
    as_text = True)
    
2.图的读取
从序列化的二进制文件中读取数据，从读取到数据中创建GraphDef对象，导入GraphDef对象到当前图中，创建出对应的图结构。