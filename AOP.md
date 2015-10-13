#1 2015-10-14 AOP讨论

讨论内容方向如下：

#1.1 从AOP拦截的时机来看待AOP

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

#1.2 角色梳理：AOP联盟、SpringAOP、Aspectj以及他们各自的职责。
#1.3 SpringAOP的整体架构设计