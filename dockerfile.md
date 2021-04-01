# Dockerfile参考手册

dockerfile是docker用于构建镜像时使用的镜像文件。

## 使用

Dockerfile是通过调用docker build命令使用的。

	
	docker build 
		[-f|--file[=PATH/Dockerfile]] 
		[-t|--tag[==[]]]
		PATH|URL|-

docker在构建镜像时，除了需要描述构建指令的Dockerfile文件外，
还需要制定一个工作目录。因为docker需要在这个工作目录中查找缺省的Dockerfile
还有Dockerfile中用到的文件。

## 文件格式

	# Comment
	INSTRUCTION arguments

Dockerfile文件由两部分组成。
一部分是注释，以井号字符开始。
另一部分是指令，指令与指令参数之间以空格分隔。

## 转译

反斜杠'\'为转移符，通常在arguments中用。
与bash一样，参数中的空格和行末的反斜杠需要转译。
美元符‘$’也需要转译，因为在Dockerfile中$是变量的前缀。


## 环境变量替换

用ENV指令声明的环境变量可以用$variable_name 或 ${variable_name}
的方式在指令参数中引用。

$variable_name和${variable_name}本质是一样的，都会被替换成变量的值。
${variable_name}使用的典型场景是引用variable后面不是空格分隔符，这时为了
明确varible_name的终结位置，就需要用大括号把variable_name包裹起来。

## FROM指令

FROM指令格式

	FROM <image_name>[:tag|@digest]

FROM指令会初始化一个新的构建阶段并为后续指令的执行指定一个基础镜像。
一个合法的Dockerfile必须以FROM指令开始。

ARG指令是唯一可能在FROM之前出现的指令

## RUN指令
RUN命令的用途是在镜像的一个新的存储层执行一条指令，并将变更提交。

	RUN <command>
	
## ARG指令

ARG指令的用途是定义变量， ARG指令定义的变量可以在docker build 中使用
--build-arg <varname>=<value> 来赋值使用。

	ARG <name>[=<default value>]

变量的生命周期是在ARG指令后才生效的。
如果在使用ARG指令前引用一个变量，这个变量的值将为空。

ARG变量和ENV变量的区别是：ENV变量是会持久化到镜像中的，而ARG变量不会。

## ENV指令

ENV指令主要功能是在镜像中写入环境变量，环境变量可以和ARG声明的变量一样
使用$varname或${varname}来引用。

	ENV <key>=<value> ...

你还可以使用 docker run --env <key>=<value>来在运行时改变env的值
ENV变量的声明可以覆盖ARG变量，ENV变量也可以以ARG变量的值作为初始值。

## COPY指令

	COPY [--chown=<user>:<group>] <src>... <dest>

COPY指令会在FROM指令指定的PATH上下文路径中查找文件，并将文件复制到镜像中的<dest>路径。

## ADD指令

	ADD [--chown=<user>:<group>] <src>... <dest>

ADD指令和COPY指令功能基本相同。
但是ADD指令的src可以是tar.gz文档，ADD指令会对tar文档进行解压操作，而COPY指令不会。
ADD指令还可以是个URL，ADD指令会自动从URL中下载文件并复制到<dest>指定的路径中。

## WORKDIR指令

WORKDIR指令用于设置RUN，CMD，ENTRYPOINT，COPY，ADD指令的工作目录。

	WORKDIR <path>

## CMD指令

CMD指令的核心目的是提供容器的缺省执行命令。
一个Dockerfile中只能配置一条CMD指令，如果有多条，只有最后一条会生效。

CMD和ENTRYPOINT的区别是：CMD指定的指令是可以被docker
	
	CMD ["命令", "参数1", ... "参数n"] // json格式，又叫执行格式
	CMD ["参数1", ... , "参数n"] // ENTRYPOINT的缺省参数
	CMD 命令 参数1 ... 参数n // shell模式

## ENTRYPONT

ENTRYPOINT与CMD最本质的区别是：

ENTRYPOINT是入口的意思，也就是你在执行docker run命令时，即便[image] 后面加上了
[CMD], [ARG] ENTRYPOINT指定的命令还会执行，
命令行上的[CMD], [ARG] 会成为ENTRYPOINT指令的参数加在尾巴上。

如果你在docker run时指定了命令，CMD的内容会被替换。
ENTRYPOINT 和 CMD联合使用时，CMD为ENTRYPOINT的缺省参数。
ENTRYPOINT指令有两种格式：
1. 执行模式：
	
	
	ENTRYPOINT ["命令", "参数1", .... , "参数n"]

2. shell格式：
	

	ENTRYPOINT 命令 参数1 。。。参数n

执行模式是不需要启动bash来执行命令的，是推荐的格式。



## LABEL

LABEL指令是用于往镜像中添加源数据的。
格式如下：
	LABEL <关键字>=<值> ...

在Docker 1.10前用多条LABEL指令会导致镜像大小增大，但现在已经没有问题了。

如果在关键值或值中出现了空格，你需要用反斜杠\转译空格或双引号来把整个key，或value包含起来。





	


