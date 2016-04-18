在通过 JDBC 读写数据库之前需要先打开一个数据库的连接。本文将展示怎样来打开数据库的连接。

### Loading the JDBC Driver
在打开数据库连接之前需要先加载数据库驱动。事实上，从 Java 6 之后就不需要加载驱动了，但加载了也没有什么坏处。可以通过这样来加载 JDBC 驱动：

    Class.forName("driverClassName");
    
每个 JDBC 驱动都有一个基本的驱动类，这个基本的驱动类在加载的时候会初始化驱动。例如，加载 H2 数据库驱动时可以这样写：

    Class.forName("org.h2.Driver");

驱动类只需要加载一次即可，不需要在每次打开连接之前都加载它。只有在第一次打开连接时需要加载驱动类，以后就不需要了。
### Opening the Connection
可以使用 java.sql.DriverManager 类来打开数据库的连接。像这样，调用 getConnection() 方法：
    
    String url = "jdbc:mysql://localhost:3306/mybatis-demo";
    String user = "root";
    String password = "123456";
    Connection connection = DriverManager.getConnection(url, user, password);

url 是连接数据的 url 。不同的数据库的 url 格式不同，应该查询相关的文档来确定其 url 。上面显示的 url 是连接 mysql 数据库的 url 。
user 是数据库的用户名，password 是数据库的密码。

Closing the Connection
一旦使用完数据库连接之后应该立即关闭。像这样，可以通过 Connection.close() 方法来关闭连接：

    connection.close();

    
