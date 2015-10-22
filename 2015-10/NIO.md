#1 Java原生NIO类库

##1.1 BIO的问题

##1.2 引入NIO，基本示例

基本概念：

-	Channel
-	Buffer
-	Selector

Channel实现类：

-	FileChannel
-	DatagramChannel
-	SocketChannel
-	ServerSocketChannel

Buffer实现类：

-	ByteBuffer
-	CharBuffer
-	DoubleBuffer
-	LongBuffer

![Channel和Buffer的关系](https://static.oschina.net/uploads/img/201510/22201601_paey.png "Channel和Buffer的关系")

Buffer原理介绍

-	capacity,position和limit工作原理
-	rewind()方法
-	clear()与compact()方法
-	mark()与reset()方法

##1.3 Socket类库

##1.4 BIO NIO AIO简单对比

#2 Reactor线程模型

##2.1 传统Socket编程模型

##2.2 Reactor单线程模型

##2.3 Reactor多线程模型

#3 Netty线程模型

主要讲解这篇文章[Netty系列之Netty线程模型](http://www.infoq.com/cn/articles/netty-threading-model)


