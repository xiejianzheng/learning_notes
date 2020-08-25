# maven使用

	mvn [选项] [目标...] [阶段...]

## maven选项

-D
	定义一个系统属性
	如 -DskipTests 表示定义一个skipTests的系统属性值为true；
	如果想把skipTests定义为false，需要这样写-DskipTests=false。
	因为当你定义一个布尔变量时如果不写=value，maven缺省会将其认为是0。


## surefire编译插件
	surefire插件是junit的运行插件。上面的skipTests参数就是由surefire插件提供使用的。
	surefire在英文中是确保的意思，test passed就是surefire的前提。




