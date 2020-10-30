# 时间日期

## LocalDateTime

1. 不可改变的本地时间类型。

2. 获取年： int getYear()
3. 获取月： Month getMonth()		Month是枚举类型 需要用getValue()函数来获取对应的整型值
4. 获取日： int getDayOfMonth()

5. 获取时： int getHour()
6. 获取分:  int getMinute()
7. 获取秒： int getSecond()

## Duration

1. 计算时间差： Duration.between(datetime1, datetime2)
2. 将时间差转换为微秒： toMillis()

# 集合类型

## NavigableSet

1. ceiling(E e) 	（天花板）	返回这个集合中大于或等于这个元素的最小元素

2. floor(E e)		（地板）	返回这个集合中小于或等于这个元素的最大元素

3. higher(E e)		（更高）	返回这个集合中严格大于给定元素的最小元素

4. lower(E e)		（更小） 	返回这个集合中严格小于给定元素的最大元素


## BlockingQueue
BlockingQueue

# 文件相关操作

java8中nio的Files类提供了大量文件常见操作api。

## Path

java8中的用于描述文件位置的类。

1. Path.of(String first, String... more) 	从一个或一序列路径字符串拼接成一个路径对象

## Files

1. writeString(Path path, CharSequence csq, OpenOption... options) 把一串字符串写入文件中

OpenOption为文件打开选项，它是一个空借口，大概是用来标识实现了有两个实现类。一个是StandardOpenOption一个是LinkOption都是枚举类。

OptionOption包含：

* READ
* WRITE
* APPEND
* TRUNCATE_EXISTING
* CERATE
* CREATE_NEW
* DELETE_ON_CLOSE
* SPARSE
* SYNC
* DSYNC

# 执行器接口

## Executor接口

Executor接口用于执行Runnable对象的。Executor接口提供了一种分离任务提交和任务执行的机制。
任务的创建者只负责提交任务，任务的线程使用、调度细节都由Executor接口内部实现。

Executor接口只有一个方法：

	void execute(Runnable command)

## ExecutorService接口

ExecutorService接口是Executor接口的扩展，提供管理任务终止和为一个或多个任务返回执行进度的Future类的接口。

ExecutorService接口就是一个强化的执行器，也就可以成为服务化的执行器。

他提供了：

1. 提交任务接口：	Future<?> submit(Runnable task)

2. 批量执行任务接口:	<T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks)


## Executors类

提供了创建各种各样Executor和ExecutorService的工厂方法和executor相关的工具类。

如：
1. 创建单线程执行器的方法：	static ScheduledExecutorService newSingleThreadExecutor()
2. 

# 数据库访问接口

## DataSource接口

## PreparedStatement接口

PreparedStatement翻译过来就是预编译语句的意思。PreparedStatement主要用于更有效地执行多遍语句上面。

PreparedStatement由连接对象的prepareStatement(String sql) 构建。

1. executeBatch
	
	用于批量执行sql命令。

2. addBatch
	向此PreparedStatement对象的批量命令中添加一个参数集合。










