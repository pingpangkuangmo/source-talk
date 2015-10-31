#1 参考文章

-	[并发编程网：Java NIO系列教程](http://ifeve.com/socket-channel)
-	[infoq:Netty系列之Netty线程模型](http://www.infoq.com/cn/articles/netty-threading-model)
-	[infoq:Java NIO通信框架在电信领域的实践](http://www.infoq.com/cn/articles/practice-of-java-nio-communication-framework)
-	[经典tcp粘包分析](http://www.cnblogs.com/zhaox583132460/p/3372381.html)
-	[Mina、Netty、Twisted一起学](http://blog.csdn.net/column/details/mina-netty-twisted.html)

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
-	SelectorProvider,用于提供Selector实现,而自身靠系统属性或者SPI机制来加载

要学会的案例：

-	1 不使用Selector的情况下，非阻塞式的socket编程
-	2 使用Selector的情况下，socket的无阻塞式编程（有了前者才能更好的体会出Selector的好）


ZooKeeper中就是使用的原生的NIO Socket类库来实现NIO通讯，展示：

![ZooKeeper NIO通讯](https://static.oschina.net/uploads/img/201510/29084554_s23M.png "ZooKeeper NIO通讯")
![ZooKeeper NIO通讯](https://static.oschina.net/uploads/img/201510/29084702_84Lh.png "ZooKeeper NIO通讯")

##1.4 BIO NIO AIO简单对比总结

#2 Reactor线程模型

##2.1 传统BIO模型

![传统BIO模型](https://static.oschina.net/uploads/img/201510/20083738_I5mX.png "传统BIO模型")

##2.2 Reactor单线程模型

![Reactor单线程模型](https://static.oschina.net/uploads/img/201510/31082759_7QTr.png "Reactor单线程模型")

##2.3 Reactor多线程模型

![Reactor多线程模型](https://static.oschina.net/uploads/img/201510/20083315_ObVg.png "Reactor多线程模型")

##2.4 Reactor主从多线程模型

![Reactor主从多线程模型](https://static.oschina.net/uploads/img/201510/31083225_mNIH.png "Reactor主从多线程模型")

#3 网络通信问题

-	tcp粘包以及封包和拆包，见[经典tcp粘包分析](http://www.cnblogs.com/zhaox583132460/p/3372381.html)，对于此问题常见的解决办法，使用固定的消息长度、使用分隔符、使用固定长度的Header和Body组合
-	使用固定的Header和Body组合来定制自己的协议，如dubbo协议

	![dubbo协议](https://static.oschina.net/uploads/img/201510/31090546_37Uy.png "dubbo协议")

-	编解码问题和序列化问题

	

#4 Netty使用案例及源码分析


主要讲解这篇文章[Netty系列之Netty线程模型](http://www.infoq.com/cn/articles/netty-threading-model)

