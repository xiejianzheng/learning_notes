# MyBatis使用指南

## MyBatis的核心：Sql会话工厂（SqlSessionFactory）

Sql会话工厂是MyBatis应用的核心。
Sql会话工厂是通过Sql会话工厂构造器(SqlSessionFactoryBuilder)构造的。

Sql会话工厂构造器可以通过配置对象（Configuration）或Xml配置文件来生成Sql会话工厂。
如：
	
	String resource = "org/mybatis/example/mybatis-config.xml"
	InputStream inputStream = Resources.getResourceAsStream(resource);
	SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

对于MyBatisSpringBootStarter来说，Sql会话工厂是由Spring来创建的。
Spring还会自动检测你的Mapper，并把它关联到Spring自己实现的Sql会话对象：SqlSessionTemplate。

## Spring的MyBatis配置属性

在application.yml的mybatis区域下，spring支持如下几个配置：


1. mapper-locations： mapper映射xml文件的路径， 可以是classpath

如： 

	classpath:mapper/*.xml

2. type-aliases-package: 类型别名的包名配置

如：com.xxx.bean


## MyBatis映射文件结构

第一行是xml文档的声明。其实是名为xml的处理指令。
处理指令的格式为

	<?处理指令 处理指令信息?>
	
xml的声明包括version和encoding
version一般="1.0"
encoding一般为"UTF-8"

第二行是xml文档对应的文档类型定义
可以把它理解为一个元素
元素名为!DOCTYPE
!DOCTYPE元素的格式为：

	<!DOCTYPE 根节点 文档定义文件所属空间。。。。

如果文档定义文件所属空间为PUBLIC, 着文档定义节点后续的两个参数为
1. 文档定义文件名
2. 文档定义文件路径

"-//mybatis.org/DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd"

## 映射器文档结构

### 根节点：映射器 mapper

xml的根节点mapper表示了当前xml文件声明的是MyBatis映射器的配置。

mapper下面有

	resultMap
	sql
	insert
	update
	delete
	select
等元素用于描述：
* sql到java方法映射
* sql查询结果集到java实体对象映射

#### sql元素
用于声明一个sql片段，为了后续引用 需要给sql片段设置一个id属性。
后续引用时使用include元素并用refid属性指定sql片段。

需要声明“名字空间”字段。
名字空间字段对应了一个java接口。
MyBatis会将Mapper中声明的select元素映射为方法。


### resultMap结果映射

结果映射是用于将数据库返回的结果集映射到java对象的属性上的xml声明元素

属性:
* id: 用于后续在select、insert、delete、update等元素中引用结果集映射规则。
* type: 表示resultMap绑定的java实体类类型

子元素：
* id 用于映射sql查询结果集的唯一标识到java类属性。
* result 用于映射sql结果集中的普通列到java类属性。

id或result元素的属性包含：
* property 表示结果集当前列需要映射到的java类属性名。
* column 表示当前映射元素绑定的sql结果集列名。
* jdbcType


## 动态SQL

### 参数

在动态SQL中，MyBatis支持接收从函数中获取参数值，并把它转换到sql中。

如果要引用一个参数值，需要使用如下符号：
	#{参数名}
	
### if元素

if元素用于有条件地将sql片段加入到sql语句中。

if元素的属性包括：
* test: 用于描述if元素的条件

test属性中可以直接使用当前所处的语句元素中存在的参数来做值判断。
在test属性引用参数时，无需像在元素的内容块中引用参数那样使用#{}来圈住要引用的参数。

## typeAliases
一个类型别名只是一个简单的名为了Java类型。
它只与XML配置相关，简单存在只是为了减少冗余的打字属于完全限定类名称。
例如
