在运行时，Class 对象也可以被作为类型规范。例如，可以像这样来创建一个泛型方法：

    public static <T> T getInstance(Class<T> theClass)
    throws IllegalAccessException, InstantiationException {
		return theClass.newInstance();
    }

下面是个调用 getInstance() 方法的例子：

	String string = getInstance(String.class);
	MyClass myClass = getInstance(MyClass.class);
注意，class 必须要有默认的构造方法，例如 MyClass 就必须要有默认的构造方法，如果没有默认构造方法会报 java.lang.InstantiationException 异常，不管是直接创建对象还是间接创建对象都得依赖构造方法，newInstance() 会调用默认构造方法来实例化对象。

可以看到 getInstance() 方法返回的对象类型依赖于传递给 getInstance() 方法的参数。这对于数据库 API 来说是很方便，例如 从数据库读取对象再使用 Butterfly（是作者独立开发的一个持久化框架） 持久化框架把数据库中的记录转变为对象。下面是 method 定义的一个例子：

	public static <T> T read(Class<T> theClass, String sql)
	throws IllegalAccessException, InstantiationException {
		// 执行 sql
		T o = theClass.newInstance();
		// 通过反射设置属性。
		return o;
    }

下面是 read() 方法的使用方式：

	Driver employee = read(Driver.class, "select * from drivers where id=1");
	Vehicle vehicle = read(Vehicle.class, "select * from vehicles where id=1");

很巧妙，是不是？