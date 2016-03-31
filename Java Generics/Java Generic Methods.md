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
Integer，第二个参数的 Collection 的泛型类型也必须是 Integer 。编译器是从参数 T 的类型和 collection<T> 的参数定义中知道的，方法返回的类型是 T ，传参的类型也是 T ，所以返回的类型和传参的类型是一致的，而编译器可以知道传参的类型，当然就可以知道返回值的类型。参数在运行时也会携带着类型信息。

编译器甚至可以执行更高级的类型推断，例如，下面的调用也是合法的：

    String stringElement = "stringElement";
    List<Object> objectList = new ArrayList<Object>();
    
    Object theElement = addAndReturn(stringElement, objectList);
    
在上面的例子中，T 有两种不同的类型：String 和 Object 。在这种情况下，编译器会选择最特殊的参数类型作为 T 的类型，保证方法调用之后返回的类型是正确的。在上面的例子中，编译器会推导出 T 的类型为 Object （我自己的补充，在出现多种类型时，只有这几种类型之间具有父子关系编译器才会选用父类型作为 T 的类型，如果类型之间没有父子关系，编译器应该会报错，比如一种类型是 String ，另一种类型是 Integer）。

把参数的类型调换一下却是不合法的：

    Object objectElement = new Object();
    List<String> stringList = new ArrayList<String>();
    Object theElement = addAndReturn(objectElement, stringList);
    
在上面的推导中，编译器为了确保方法调用是类型安全的，T 只能是 String ，传递给行参 T element 的 objectElement 的类型也必须是 String 类型，而 objectElement 的类型是 Object ，Object 也不是 String 的子类，所以编译器会报错。
注意，List<String> 不是 List<Object> 的子类型，所以能出现 List<Object> 的地方不一定能出现 List<String> 。
     
    
    


    
