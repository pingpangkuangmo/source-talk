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

#3 角色梳理：AOP联盟、Aspectj、SpringAOP以及他们各自的职责。

#3.1 AOP的概念

-	Pointcut：切入点，表示在哪里进行拦截，简单理解如正则表达式
-	Joinpoint：连接点，符合上述正则表达式的一个具体对象
-	Advice：增强，即拦截逻辑

	Advice的类型：

	-	1 前置增强（Before advice）
	-	2 后置返回增强（After returning advice）
	-	3 后置异常增强（After throwing advice）
	-	4 环绕增强（Around Advice）
	-	5 引入增强（对类进行增强）

-	Aspect：切面，包含切入点和增强
-	Target Object：要代理的目标对象
-	AOP Proxy：代理对象
-	Weaving：织入，可以是编译期、字节码加载前、字节码加载后


#3.2 Aspectj

这里有个系列文章[跟我学aspectj](http://blog.csdn.net/zl3450341/article/category/1169602)

-	在编译时期就织入
-	不能使用传统的JDK编译
-	等等

#4 SpringAOP的发展历程

##4.1 JDK和CGLib动态代理的原始方式

JDK动态代理：

![JDK动态代理](https://static.oschina.net/uploads/img/201510/14195043_yBgL.png "JDK动态代理")

CGLib动态代理：

![CGLib动态代理](https://static.oschina.net/uploads/img/201510/14195135_cuGv.png "CGLib动态代理")
	
##4.2 ProxyFactory对jdk和cglib的封装

ProxyFactory简单的对jdk和cglib的封装，根据配置（强制采用cglib）或者自行决定（根据是否实现接口）采用jdk动态代理还是cglib动态代理。

对jdk动态代理的封装：

InvocationHandler h：固定是JdkDynamicAopProxy，其中InvocationHandler的接口方法Object invoke(Object proxy, Method method, Object[] args)实现如下：

![JdkDynamicAopProxy对InvocationHandler的实现](https://static.oschina.net/uploads/img/201510/14201123_NL6U.png "JdkDynamicAopProxy对InvocationHandler的实现")






问题是：

-	一个ProxyFactory只能代理一个目标对象target
-	对于


##4.3 

为了对某些方法进行拦截，引入切面Aspect（包含了增强Advice和切入点Pointcut），使用切入点来选择要拦截的方法

切面可以是：

-	正则表达式类型 JdkRegexpMethodPointcut
-	aspectj的pointcut表达式类型，如
	
		execution(* com.aspectj.demo.test.HelloWorld.main(..))
		@annotation(aop.demo.Tag)

##4.4 批量代理

上述ProxyFactory还只能针对某一个target进行代理。为了对符合pointcut条件的某一批类都进行AOP代理，引入AbstractAutoProxyCreator来进行批量处理。对于每一个对象仍然采用ProxyFactory来进行代理

![AbstractAutoProxyCreator批量代理](https://static.oschina.net/uploads/img/201510/14194847_TxWI.png "AbstractAutoProxyCreator批量代理")

#5 强烈推荐文章

-	[AOP 那点事儿](http://my.oschina.net/huangyong/blog/161338) 黄勇
-	[AOP 那点事儿（续集）](http://my.oschina.net/huangyong/blog/161402) 黄勇
-	[我对AOP的理解](http://jinnianshilongnian.iteye.com/blog/1474325)   开涛
-	[AOP实现机制](http://www.iteye.com/topic/1116696) fantasy
-	[跟我学aspectj](http://blog.csdn.net/zl3450341/article/category/1169602) 兔子党-大胡子