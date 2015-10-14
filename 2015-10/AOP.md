#1 2015-10-14 AOP讨论

讨论内容方向如下：

#2 从AOP拦截的时机来看待AOP

-	编译期
-	字节码加载前
-	字节码加载后

如图：

![AOP实现机制分类](https://static.oschina.net/uploads/img/201510/13204830_XUbN.png "AOP实现机制分类")

-	1 aspectj : 在编译期静态植入
-	2 JDK Proxy: 目标类加载后，为其接口动态生成代理类
-	3 cglib : 目标类加载后，为其动态生成子类，将切面逻辑加入子类中
-	4 自定义类加载器：在目标类加载前，将切面逻辑加入目标类字节码中
-	5 字节码转换器：在目标类加载前，将切面逻辑加入目标类字节码中（jdk1.5的Instrumentation）；在目标类加载后，将切面逻辑加入目标类字节码中（jdk1.6的Instrumentation触发jvm重新类加载）

#3 角色梳理：AOP联盟、SpringAOP、Aspectj以及他们各自的职责。

#3.1 AOP的概念

-	Pointcut：切入点，表示在哪里进行拦截，简单理解如正则表达式
-	Joinpoint：连接点，符合上述正则表达式的一个具体对象
-	Advice：增强，即拦截逻辑

	Advice的类型：

	-	1 前置增强（Before advice）
	-	2 后置返回增强（After returning advice）
	-	3 后置异常增强（After throwing advice）
	-	4 环绕增强（Around Advice）

-	Aspect：切面，包含切入点和增强
-	Target Object：要代理的目标对象
-	AOP Proxy：代理对象
-	Weaving：织入，可以是编译期、字节码加载前、字节码加载后


#3.2 

#4 SpringAOP的整体架构设计


#5 推荐文章

-	[AOP 那点事儿](http://my.oschina.net/huangyong/blog/161338) 黄勇
-	[AOP 那点事儿（续集）](http://my.oschina.net/huangyong/blog/161402) 黄勇
-	[我对AOP的理解](http://jinnianshilongnian.iteye.com/blog/1474325)   开涛
-	[AOP实现机制](http://www.iteye.com/topic/1116696) fantasy