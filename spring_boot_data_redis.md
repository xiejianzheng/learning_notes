# 为什么要使用Spring Data Redis

因为Spring Boot Redis框架通过Spring出色的基础设施的支持，消除了与存储交互所需的冗余任务和样板代码，
使编写使用Redis键值存储的Spring应变得更加容易。

# 对Redis的支持

## 支持高级视图

Spring Data Redis提供了多个组件，对于大多数任务，高级抽象和支持服务是最佳选择。
但是，在任何时候，你都可以在层间移动。例如，你可以获取一个底层连接（甚至本地库)直接与redis通信。

## 连接到redis

使用redis和spring时的首要任务之一就是通过IoC容器连接到存储。为此，Java连接器（或绑定）是需要的。
不管你选择的库是什么，你只需要使用一组Spring Data Redis api(它在所以连接器中的行都是一致的）：
org.springframework.data.redis.connection包和它下面的RedisConnection和RedisConnectionFactory接口
用于工作和检索到redis的活动连接。

### RedisConnection 和 RedisConnectionFactory

RedisConnection为Redis通信提供了核心构建模块，因为处理与Redis后端的通信。
它还自动将底层连接库异常转换转换为Spring的一致DAO异常层次结构，
这样你就可以在不更该任何代码的情况下切换连接器，因为操作语义不变。

活动的RedisConnection对象

