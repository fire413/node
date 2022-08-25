# Spring Boot #
SpringBoot可以简单地看成简化了的、按照约定开发的SSM(H), 开发速度大大提升。 可是呢，最好还是有 SSM(H)的基础，否则其中用到了Spring MVC,Mybatis,Hibernate的地方，或觉得摸不着头脑。
### SSM(H) ###
SSM指的是Spring、Struts、MyBatis三种框架，H指的是Hibernate。
## Spring ##
Spring是一个基于IOC和AOP的结构J2EE系统的框架 
IOC 反转控制 是Spring的基础，Inversion Of Control 
简单说就是创建对象由以前的程序员自己new 构造方法来调用，变成了交由Spring创建对象
DI 依赖注入 Dependency Inject. 简单地说就是拿到的对象的属性，已经被注入好相关值了，直接使用即可。
#### IOC ####
[控制反转](https://baike.baidu.com/item/控制反转/1158025?fromtitle=ioc&fromid=4853&fr=aladdin "控制反转")（Inversion of Control，缩写为IoC），是面向对象编程中的一种设计原则，可以用来减低计算机代码之间的耦合度。其中最常见的方式叫做依赖注入（Dependency Injection，简称DI），还有一种方式叫“依赖查找”（Dependency Lookup）。通过控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体将其所依赖的对象的引用传递给它。也可以说，依赖被注入到对象中。
## Spring MVC ##
[tomcat三大部署项目方式](https://blog.csdn.net/sinat_32366329/article/details/80261706)
创建项目的步骤：<br />
1. 在eclipse中使用dynamic web project的方式<br />
2. 导入jar包，把文件放到项目的WebContent/WEB-INF/lib的目录下<br />
3. 在WEB-INF目录下创建web.xml<br />
4. 在WEB-INF目录下创建springmvc-servlet.xml<br />
5. 控制类 IndexController<br />
6. 准备index.jsp<br />
7. 部署在tomcat中，重启测试<br />
 