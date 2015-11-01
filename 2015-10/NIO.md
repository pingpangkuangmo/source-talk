#1 2015-11-01 NIO讨论

-	[并发编程网：Java NIO系列教程](http://ifeve.com/socket-channel)
-	[infoq:Netty系列之Netty线程模型](http://www.infoq.com/cn/articles/netty-threading-model)
-	[infoq:Java NIO通信框架在电信领域的实践](http://www.infoq.com/cn/articles/practice-of-java-nio-communication-framework)
-	[经典tcp粘包分析](http://www.cnblogs.com/zhaox583132460/p/3372381.html)
-	[Mina、Netty、Twisted一起学](http://blog.csdn.net/column/details/mina-netty-twisted.html)
-	[理解Java NIO](http://my.oschina.net/regulusun/blog/137819)
-	[Netty系列之Netty编解码框架分析](http://www.infoq.com/cn/articles/netty-codec-framework-analyse)

#2 Java原生NIO类库

##2.1 BIO的问题

InputStream的读取和写入问题

-	同步异步和阻塞非阻塞的区别
-	NIO是非阻塞式IO吗？怎么体现出非阻塞的呢？

##2.2 引入NIO，基本示例

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

##2.3 Socket类库

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

##2.4 BIO NIO AIO简单对比总结

#3 Reactor线程模型

##3.1 传统BIO模型

![传统BIO模型](https://static.oschina.net/uploads/img/201510/20083738_I5mX.png "传统BIO模型")

##3.2 Reactor单线程模型

![Reactor单线程模型](https://static.oschina.net/uploads/img/201510/31082759_7QTr.png "Reactor单线程模型")

##3.3 Reactor多线程模型

![Reactor多线程模型](https://static.oschina.net/uploads/img/201510/20083315_ObVg.png "Reactor多线程模型")

##3.4 Reactor主从多线程模型

![Reactor主从多线程模型](https://static.oschina.net/uploads/img/201510/31083225_mNIH.png "Reactor主从多线程模型")

#4 Netty使用案例及源码分析

主要讲解这篇文章[Netty系列之Netty线程模型](http://www.infoq.com/cn/articles/netty-threading-model)

-	1 每一个NioEventLoop：包含一个线程和一个Selector selector复用器

	因此一个NioEventLoop就可以处理很多链路，每个链路的读写操作全部交给这一个线程来处理，避免了并发操作同一个链路的可能性

	![NioEventLoop处理](https://static.oschina.net/uploads/img/201511/01202038_1gFO.png "NioEventLoop处理")

-	2 每当有一个新的客户端接入，则从NioEventLoop线程组中顺序获取一个可用的NioEventLoop，当到达数组上限之后，重新返回到0，通	过这种方式，可以基本保证各个NioEventLoop的负载均衡。一个客户端连接只注册到一个NioEventLoop上，这样就避免了多个IO线程去	并发操作它

#5 网络通信问题

-	tcp粘包以及封包和拆包，见[经典tcp粘包分析](http://www.cnblogs.com/zhaox583132460/p/3372381.html)，对于此问题常见的解决办法，使用固定的消息长度、使用分隔符、使用固定长度的Header和Body组合
-	使用固定的Header和Body组合来定制自己的协议，如dubbo协议

	![dubbo协议](https://static.oschina.net/uploads/img/201510/31090546_37Uy.png "dubbo协议")

-	编解码问题和序列化问题

	-	使用固定长度的消息
	-	使用分隔符
	-	使用固定长度的Header加Body的形式

编解码需要处理半包问题，而序列化则不用关心，序列化专注于byte数组和对象之间的相互转化

在dubbo中，编解码器用于处理Header部分，序列化框架用于处理Body部分

![dubbo的编解码和序列化](https://static.oschina.net/uploads/img/201511/01174647_lnBz.jpg "dubbo的编解码和序列化")

#6 还需解决的问题

-	1 同步异步和阻塞非阻塞的区别？
-	2 NIO中的非阻塞体现在哪？



