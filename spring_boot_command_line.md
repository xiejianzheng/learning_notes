# SpringBoot 命令行的处理

SpringBoot程序缺省情况下会把命令行中的所有以“-”开始的选项参数作为“属性”添加到Spring环境中去。

## 命令行读取
如果需要单独读取命令行，SpringBoot应用的主类需要实现ApplicationRunner接口。
SpringBoot在启动阶段会调用ApplicationRunner的run(ApplicationArguments args)方法。

ApplicationArguments中包含了选项参数非选项参数。

1. getNonOptionArgs() 用于获取非选项参数。
2. getOptionNames() 用于获取所有选项参数的值。
3. getOptionValues(String name)  用于获取指定选项的所有值。




