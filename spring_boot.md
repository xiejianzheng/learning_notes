# spring标注解析

## 配置文件

指定配置文件名: 加上命令行参数 --spring.config.location=<文件名>


## spring单元测试总结

如我们所知，spring中我们很多组件、配置都是采用<注解> 注入的。
在我们写的组件中也使用了这种方式注入了其他依赖组件和配置。
因此我们在对这些组件进行测试时不得不启动spring的自动依赖注入框架。

如果我们按缺省的配置启动， 会启动过多的组件。而且在做单元测试期间我们很多组件是需要mock的。

因此我们需要使用spring的 <轮廓注解> 进行进行不同的组件配置，并使用<活动轮廓注解> 进行配置选择。


## spring注解总结

@Configuration注解

	用于类上，用于声明该类是用于定义组件的。


@Bean注解
	
	用于定义spring组件，这个注解用于方法级别。
	@Bean注解@Configuration注解一起工作，用来创建Spring组件。

@Value注解

	应用于类的域，构造函数参数，还有方法参数级别。
	@Value注解标识着域或参数的缺省值会从属性文件中提取出来。
	@Value对应的占位符格式是#{属性名}或${属性名}

@Profile注解
	指示一个或多个轮廓处于活跃时，组件有资格进行注册。
	轮廓是是个逻辑分组 有3种激活方式。

	1. 使用编程的方式激活ConfigurableEnvironment.setActiveProfiles()
	2. 设置属性spring.profiles.active
	3. 使用@ActiveProfiles注解

	轮廓注解可以一下三种方式使用：
	1. 作为一个类级注解在直接或间接用@Component注解标识的类上使用。包括@Configuration。
	2. 作为元数据注解。用于编写定制的原型注解。
	3. 作为方法级注解，用于使用了@Bean标识的方式。

	轮廓注解例子：
	@Profile({"p1", "p2"}) 	表示只有p1或p1轮廓激活时，组件才能注册。
	@Profile({"p1", "!p2"})	表示只有p1激活或p2不激活时，组件才能注册。


@ActiveProfiles注解

	ActiveProfiles注解是一个类级的注解。
	用于声明在测试类时哪个活动的豆定义轮廓需要在应用上下文中加载。

	活动轮廓注解可以作为元注解用来创建定制的组合注解。


@ContextConfiguration注解
	
	@ContextConfiguration注解定义了一个类级别的元数据，用于决定如何加载和配置应用上下文为了集成测试。
	1. 可以用于声明基于路径的资源位置(通过locations() 或 value() 属性)。
	2. 可以用于声明基于组件类(通过classes()属性)

@TestPropertySource注解

	测试属性源注解是一个类级别的注解。用于配置属性文件 **位置** 和内联的 **属性**， 用于添加到环境的中的


#SpringBoot注解总结

@EnableAutoConfiguration注解

	@EnableAutoConfiguration注解用于激活Spring应用上下文的自动配置功能。 尝试




