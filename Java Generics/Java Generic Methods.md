在 Java 中也可以泛型化方法，下面是一个例子：

    public static <T> T addAndReturn(T element, Collection<T> collection) {
        collection.add(element);
        return element;
    }
    
这个方法定义了一个类型 T ，T 是 element 的参数类型同时也是 Collection 的泛型类型。
注意，现在可以往集合里添加元素了。在集合的参数定义处使用通配符，往集合里添加元素编译器就会报错。
那么，编译器是如何知道 T 的类型的呢？
答案是，编译器会根据你使用的 class 中的 method 来推导类型。例如：

    String stringElement = "stringElement";
    List<String> stringList = new ArrayList<String>;
    
    String theStringElement = addAndReturn(stringElement, stringList);
    
    Integer integerElement = new Integer(123);
    List<Integer> integerList = new ArrayList<Integer>();
    
    Integer theIntegerElement = addAndReturn(integerElement, integerList);
    
注意，在调用 addAndReturn() 方法时第一个参数的类型是 String ，第二个参数 Collection 的泛型类型也必须是 String，在第二次调用 addAndReturn() 方法时第一个参数的类型是
Integer，第二个参数的 Collection 的泛型类型也必须是 Integer 。    
