#1 参考文章

-	[并发编程网：Java NIO系列教程](http://ifeve.com/socket-channel)

#1 Java原生NIO类库

##1.1 BIO的问题

InputStream的读取和写入问题

##1.2 引入NIO，基本示例

基本概念：

-	Channel
-	Buffer

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

-	DatagramChannel
-	SocketChannel
-	ServerSocketChannel
-	Selector

要学会的案例：

-	1 不使用Selector的情况下，非阻塞式的socket编程
-	2 使用Selector的情况下，socket的无阻塞式编程（有了前者才能更好的体会出Selector的好）


ZooKeeper中就是使用的原生的NIO Socket类库来实现NIO通讯，展示：

![ZooKeeper NIO通讯](https://static.oschina.net/uploads/img/201510/29084554_s23M.png "ZooKeeper NIO通讯")
![ZooKeeper NIO通讯](https://static.oschina.net/uploads/img/201510/29084702_84Lh.png "ZooKeeper NIO通讯")

##1.4 BIO NIO AIO简单对比总结

#2 Reactor线程模型

##2.1 传统Socket编程模型

##2.2 Reactor单线程模型

##2.3 Reactor多线程模型

#3 Netty线程模型

主要讲解这篇文章[Netty系列之Netty线程模型](http://www.infoq.com/cn/articles/netty-threading-model)


