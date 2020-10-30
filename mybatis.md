# MyBatis使用指南

## MyBatis的核心：Sql会话工厂（SqlSessionFactory）

Sql会话工厂是MyBatis应用的核心。
Sql会话工厂是通过Sql会话工厂构造器(SqlSessionFactoryBuilder)构造的。

Sql会话工厂构造器可以通过配置对象（Configuration）或Xml配置文件来生成Sql会话工厂。

对于MyBatisSpringBootStarter来说，Sql会话工厂是由Spring来创建的。
Spring还会自动检测你的Mapper，并把它关联到Spring自己实现的Sql会话对象：SqlSessionTemplate。

## Spring的MyBatis配置属性

在application.yml的mybatis区域下，spring支持如下几个配置：


1. mapper-locations： mapper映射xml文件的路径， 可以是classpath

如： classpath:mapper/*.xml

2. type-aliases-package: 类型别名的包名配置

如：com.xxx.bean




