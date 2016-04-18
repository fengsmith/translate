#####JDBC API 的核心部分：

- JDBC Drivers
- Connections
- Statements
- Result Sets

#####四种基本的 JDBC 使用场景：
- Query the database
- Query the database meta data
- Update the database
- Perform transactions

在接下来的部分中我会解释每一种组件及其常用使用场景。

###JDBC 的核心组件
### JDBC Drivers
JDBC 驱动是一个 Java 类的集合，通过它可以使你的应用连接到特定的数据库。例如，MySQL 数据库有它自己的 JDBC 驱动。JDBC 驱动实现了许多 JDBC 接口。具体的 JDBC 的使用都隐藏在 JDBC 接口之后。
因此，你可以换一个新的 JDBC 驱动，而代码根本感知不到驱动已经更换了。
当然，JDBC 驱动在他们各自支持的特点上会有所不同。
### JDBC Connections
JDBC 驱动被加载和初始化后就可以连接数据库了。可以通过被加载的驱动和 JDBC API 来获取数据库的连接。应用和数据库之间的所有的交流都是通过连接来完成的。一个应用可以同时打开某个数据库的多个连接，事实上这种情况也很常见。
### Statements
Statement 是用来查询和更新数据库的，有几种不同类型的 statements 来选用。每一种 statement 对应着一种查询或更新。
### ResultSets
在数据库上执行查询后，数据库会返回给我们返回一个结果集。我们可以遍历这个结果集来读取查询的结果。

### JDBC 常用使用场景
####Query the database
最常用的使用场景就是从数据库中查询数据。从数据库中读取数据叫做查询数据库。
#### Query the database meta data
另外一个常用的使用场景是查询数据库的元数据。数据库的元数据包含了数据库本身的一些信息。例如，表的定义信息，每张表的每一列的信息，每一列的数据类型等。
#### Update the database
另一个常用的 JDBC 使用场景是更新数据库。更新数据库的意思是向数据库写入数据。换句话说，更新数据库就是添加新记录或者是修改已存在的记录。
#### Perform transactions
事物是另外一个常用的使用场景。事物聚集多个更新和查询操作为一个单一的操作。要么所有的操作都执行，要么任何一个操作都不执行。

### JDBC 组件交互图
下面是一个数据库查询操作的执行过程中核心组件之间交互的一个例子（点击图片浏览大图）：



     



