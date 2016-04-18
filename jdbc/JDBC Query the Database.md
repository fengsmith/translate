查询数据库就是搜索其数据。查询数据库需要向数据库发送 SQL statements 。为了获取 SQL statements ，需要打开数据库连接。有了打开的连接之后需要创建一个 Statement 对象，下面是创建的方法：

    Statement statement = connection.createStatement();
有了 Statement 之后可以执行 SQL 查询：

    String sql = "select * from people";
    ResultSet result = statement.executeQuery(sql);

执行查询之后会返回一个结果集。结果集中包含了 SQL 查询的结果。结果集已行的形式返回，每一行中都包含了若干列，每一列都包含着数据。
可以这样来迭代结果集中的行。
    
    while(result.next()) {
        String name = result.getString("name");
        long age = result.getLong("age");
    }
如果还有其他行，ResultSet.next() 方法会把结果集中的游标移动到下一行，并且返回 true 。如果再没有其他行则返回 false 。
在读取任何数据之前需要至少调用一次 next() 方法。在第一次调用 next() 方法之前，ResultSet 定位在第一行数据之前。
可以通过一些叫 getXXX() 的方法来获取当前行的列数据，XXX 是原生数据类型。例如：
    
    result.getString("columnName");
    result.getLong("columnName");
    result.getInt("columnName");
    result.getDouble("columnName");
    result.getBigDecimal("columnName");

想要获取哪一列的值就需要把该列的列名作为一个参数传递给相应的 getXXX() 方法。
也可以像这样传递列的索引而不是列名，注意索引的下标是从 1 开始的：

    result.getString(1);
    result.getLong(2);
    result.getInt(3);
    result.getDouble(4);
    result.getBigDecimal(5);
        
使用索引的方式来获取列的值首先得知道想要获取的列在结果集中的索引值。可以通过调用 ResultSet.findColumn("columnName") 方法来获取某一列的索引值：

    int columnIndex = result.findColumn("columnName");

如果结果集中有大量的行需要迭代的话通过使用索引值要比使用列名要快。
迭代完结果集之后需要关闭 ResultSet 和 Statement，像这样，可以通过 close() 方法来关闭：
     
     result.close();
     statement.close();

当然了，关闭方法应该放到 finally 块中来执行以保证即使在迭代的过程中发生了异常，ResultSet 和 Statement 仍然能被关闭。

### 完整的例子
下面是一个完整的查询代码例子：

	Statement statement = connection.createStatement();

	String sql = "select * from people";

	ResultSet result = statement.executeQuery(sql);

	while(result.next()) {

					String name = result.getString("name");
					long   age  = result.getLong("age");

					System.out.println(name);
					System.out.println(age);
	}

	result.close();
	statement.close();
	
下面是又一个例子，这个例子添加了 try-finally 代码块，为了使代码更简短我把 catch 代码块省略了：
	
	Statement statement = null;

	try{
					statement = connection.createStatement();
					ResultSet result    = null;
					try{
									String sql = "select * from people";
									ResultSet result = statement.executeQuery(sql);

									while(result.next()) {

													String name = result.getString("name");
													long   age  = result.getLong("age");

													System.out.println(name);
													System.out.println(age);
									}
					} finally {
									if(result != null) result.close();
					}
	} finally {
					if(statement != null) statement.close();
	}

    	
     
        
    
    