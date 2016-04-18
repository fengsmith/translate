更新数据库需要使用 Statement 。但不是用 executeQuery() 方法而是用 executeUpdate() 方法。
有两种数据库更新类型：

- 更新记录的值
- 删除记录
 
两种数据库更新方式都用 executeUpdate() 方法。

### Updating Records
下面是一个更新记录值的例子：

	Statement statement = connection.createStatement();

	String    sql       = "update people set name='John' where id=123";

	int rowsAffected    = statement.executeUpdate(sql);
statement.executeUpdate(sql) 方法调用后返回的值 rowsAffected 代表了执行了这条语句后数据库中共有多少条记录被影响了。

### Deleting Records
下面是一个删除记录的例子：

	Statement statement = connection.createStatement();

	String    sql       = "delete from people where id=123";

	int rowsAffected    = statement.executeUpdate(sql);
	
同样的，statement.executeUpdate(sql) 方法调用后返回的值 rowsAffected 代表了执行了这条语句后数据库中共有多少条记录被影响了。	
	
	